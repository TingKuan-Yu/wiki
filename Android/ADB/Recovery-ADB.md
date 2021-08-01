# Issue
- adb: device unauthorized.
```
tingkuanyu@TonyYuLinux1:/D/c1/11/main/hlos_vendor_0726/out/target/product/duo2$ adb reboot recovery
tingkuanyu@TonyYuLinux1:/D/c1/11/main/hlos_vendor_0726/out/target/product/duo2$ adb devices
List of devices attached
SF857BCE29A152	unauthorized

tingkuanyu@TonyYuLinux1:/D/c1/11/main/hlos_vendor_0726/out/target/product/duo2$ adb shell
adb: device unauthorized.
This adb server's $ADB_VENDOR_KEYS is not set
Try 'adb kill-server' if that seems wrong.
Otherwise check for a confirmation dialog on your device.
```

# limitation
---
## system/core/adb/daemon/main.cpp
- Only userdebug build or unlocked devices allow access without authorization.
```
    // If we're on userdebug/eng or the device is unlocked, permit no-authentication.
    bool device_unlocked = "orange" == android::base::GetProperty("ro.boot.verifiedbootstate", "");
    if (__android_log_is_debuggable() || device_unlocked) {
        auth_required = android::base::GetBoolProperty("ro.adb.secure", false);
    }
```

# sys.usb.configfs
## device/surface/duo2/duo2.mk
- copy init.recovery.surfaceduo2.rc to recovery
```
PRODUCT_COPY_FILES += $(LOCAL_PATH)/init.recovery.hardware.rc:recovery/root/init.recovery.surfaceduo2.rc
```
## init.recovery.surfaceduo2.rc
- Set sys.usb.configfs to enable adb.
```
on init
    write /sys/class/backlight/panel0-backlight/brightness 200
    setprop sys.usb.configfs 1
```

# bootable/recovery/recovery_main.cpp
```
static bool IsDeviceUnlocked() {
  
  if("orange" == android::base::GetProperty("ro.boot.verifiedbootstate", ""))
    return true;
   
  // no use event force return true. Still need authorization.
  if("true" == android::base::GetProperty("ro.boot.adb", ""))
    return true;
  else
    return false;
}


    // We start adbd in recovery for the device with userdebug build or a unlocked bootloader.
    std::string usb_config =
        fastboot ? "fastboot" : IsRoDebuggable() || IsDeviceUnlocked() ? "adb" : "none";
    std::string usb_state = android::base::GetProperty("sys.usb.state", "none");
    if (fastboot) {
      device->PreFastboot();
    } else {
      device->PreRecovery();
    }
    if (usb_config != usb_state) {
      if (!SetUsbConfig("none")) {
        LOG(ERROR) << "Failed to clear USB config";
      }
      if (!SetUsbConfig(usb_config)) {
        LOG(ERROR) << "Failed to set USB config to " << usb_config;
      }
    }

```

# build
---
## device/surface/duo2/BoardConfig.mk
- BOARD_USES_RECOVERY_AS_BOOT
```
#Enable dtb in boot image and boot image header version 3 support.
BOARD_INCLUDE_DTB_IN_BOOTIMG := true
ifeq ($(ENABLE_AB), true)
BOARD_USES_RECOVERY_AS_BOOT := true
TARGET_NO_RECOVERY := true
endif
```
## build/make/core/Makefile
- BOARD_USES_RECOVERY_AS_BOOT affects DEBUG_RAMDISK_ROOT_DIR & DEBUG_RAMDISK_SYNC_DIR
```
# ramdisk-debug.img will rsync the content from either ramdisk.img or ramdisk-recovery.img,
# depending on whether BOARD_USES_RECOVERY_AS_BOOT is set or not.
ifeq ($(BOARD_USES_RECOVERY_AS_BOOT),true)
my_debug_ramdisk_sync_dir := $(TARGET_RECOVERY_ROOT_OUT)
else
my_debug_ramdisk_sync_dir := $(TARGET_RAMDISK_OUT)
endif # BOARD_USES_RECOVERY_AS_BOOT

$(INSTALLED_DEBUG_RAMDISK_TARGET): DEBUG_RAMDISK_SYNC_DIR := $(my_debug_ramdisk_sync_dir)
$(INSTALLED_DEBUG_RAMDISK_TARGET): DEBUG_RAMDISK_ROOT_DIR := $(my_debug_ramdisk_root_dir)

```


# Recovery default property
---
- target - $(recovery_ramdisk)
```
$(recovery_ramdisk): $(MKBOOTFS) $(COMPRESSION_COMMAND_DEPS) \
:
	ln -sf prop.default $(TARGET_RECOVERY_ROOT_OUT)/default.prop
:
```
- target - $(INSTALLED_RECOVERY_BUILD_PROP_TARGET)
```
INSTALLED_RECOVERY_BUILD_PROP_TARGET := $(TARGET_RECOVERY_ROOT_OUT)/prop.default
$(INSTALLED_RECOVERY_BUILD_PROP_TARGET): \
	    $(INSTALLED_DEFAULT_PROP_TARGET) \
	    $(INSTALLED_VENDOR_DEFAULT_PROP_TARGET) \
	    $(intermediate_system_build_prop) \
	    $(INSTALLED_VENDOR_BUILD_PROP_TARGET) \
	    $(INSTALLED_ODM_BUILD_PROP_TARGET) \
	    $(INSTALLED_PRODUCT_BUILD_PROP_TARGET) \
	    $(INSTALLED_SYSTEM_EXT_BUILD_PROP_TARGET)
	@echo "Target recovery buildinfo: $@"
	$(hide) mkdir -p $(dir $@)
	$(hide) rm -f $@
	$(hide) cat $(INSTALLED_DEFAULT_PROP_TARGET) > $@
	$(hide) cat $(INSTALLED_VENDOR_DEFAULT_PROP_TARGET) >> $@
	$(hide) cat $(intermediate_system_build_prop) >> $@
	$(hide) cat $(INSTALLED_VENDOR_BUILD_PROP_TARGET) >> $@
	$(hide) cat $(INSTALLED_ODM_BUILD_PROP_TARGET) >> $@
	$(hide) cat $(INSTALLED_PRODUCT_BUILD_PROP_TARGET) >> $@
	$(hide) cat $(INSTALLED_SYSTEM_EXT_BUILD_PROP_TARGET) >> $@
	$(call append-recovery-ui-properties,$(PRIVATE_RECOVERY_UI_PROPERTIES),$@)
```