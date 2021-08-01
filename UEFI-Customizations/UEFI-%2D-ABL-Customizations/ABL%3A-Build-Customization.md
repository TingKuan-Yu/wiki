
# Qualcomm Build Flow
- **device/qcom/lahaina/AndroidBoard.mk**
```
ifneq ($(strip $(TARGET_NO_BOOTLOADER)),true)

# Compile
include bootable/bootloader/edk2/AndroidBoot.mk

$(INSTALLED_BOOTLOADER_MODULE): $(TARGET_EMMC_BOOTLOADER) | $(ACP)
#   $(transform-prebuilt-to-target)
$(BUILT_TARGET_FILES_PACKAGE): $(INSTALLED_BOOTLOADER_MODULE)

droidcore: $(INSTALLED_BOOTLOADER_MODULE)
endif
```
- ## Disable building ABL if you want
  - set TARGET_NO_BOOTLOADER := true in BoardConfig.mk

- **bootable/bootloader/edk2/AndroidBoot.mk**