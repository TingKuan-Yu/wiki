# Initial NULL display if ENABLE_NULL_DISPLAY_PROP is not false
- Refer to "HWCDisplay::Init()" in hardware/qcom/display/composer/hwc_display.cpp
- int HWCDisplay::Init()
```
  HWCDebugHandler::Get()->GetProperty(ENABLE_NULL_DISPLAY_PROP, &null_display_mode_);

  if (null_display_mode_) {
    DisplayNull *disp_null = new DisplayNull();
    disp_null->Init();
    use_metadata_refresh_rate_ = false;
    display_intf_ = disp_null;
    DLOGI("Enabling null display mode for display type %d", type_);
  }
```

# Set property to null display
- For mteos build - persist.vendor.display.enable_null_display
  - Set persist.vendor.display.enable_null_display to 1 for userdebug buid to ensable null display
- For user build - vendor.display.enable_null_display
  - Set vendor.display.enable_null_display to 1 for userdebug buid to ensable null display
    - Need to set at build time in make file.
- The related code snippet in hardware/qcom/display/include/display_properties.h
```
#define DISP_PROP_PREFIX                     "vendor.display."
#define PERSIST_DISP_PROP_PREFIX             "persist.vendor.display."

#define DISPLAY_PROP(prop_name)              DISP_PROP_PREFIX prop_name
#define PERSIST_DISPLAY_PROP(prop_name)      PERSIST_DISP_PROP_PREFIX prop_name

/*MSCHANGE start, make null display persitent for MTE*/
#ifdef PERSIST_NULL_DISPLAY
#define ENABLE_NULL_DISPLAY_PROP             PERSIST_DISPLAY_PROP("enable_null_display")
#else
#define ENABLE_NULL_DISPLAY_PROP             DISPLAY_PROP("enable_null_display")
#endif
/*MSCHANGE end*/
```

# Using persist.vendor.display. property in metos
- vendor/qcom/defs/product-defs/vendor/display-product.mk
```
#MSCHANGE start
SOONG_CONFIG_qtidisplay_persistnulldisplay := false
#Only make enable_null_display persistent for mte userdebug or eng
ifneq (,$(filter userdebug eng, $(TARGET_BUILD_VARIANT)))
    ifeq ($(MSSKU),mteos)
        SOONG_CONFIG_qtidisplay_persistnulldisplay := true
    endif
endif
```
- adb shell setprop persist.vendor.display.enable_null_display 1

# Using vendor.display. property in other builds than metos
- Patch for Makefile
```
diff --git a/core/Makefile b/core/Makefile
index 46171a1247..415a94268e 100644
--- a/core/Makefile
+++ b/core/Makefile
@@ -511,6 +511,7 @@ endif
 	$(hide) echo ro.product.board="$(TARGET_BOOTLOADER_BOARD_NAME)">>$@
 	$(hide) echo ro.board.platform="$(TARGET_BOARD_PLATFORM)">>$@
 	$(hide) echo ro.hwui.use_vulkan="$(TARGET_USES_VULKAN)">>$@
+	$(hide) echo vendor.display.enable_null_display=1>>$@
 ifdef TARGET_SCREEN_DENSITY
 	$(hide) echo ro.sf.lcd_density="$(TARGET_SCREEN_DENSITY)">>$@
 endif
```


