# Gobal
---
## PRODUCT_NAME
- name of the product
```
PRODUCT_NAME := oemc1
```
## BOARD_KERNEL_MODULE_DIRS
- Use in Makefile
- Makefile use this definition to generate ALL_DEFAULT_INSTALLED_MODULES
```
BOARD_KERNEL_MODULE_DIRS += top

$(foreach dir,$(BOARD_KERNEL_MODULE_DIRS), \
  $(eval ALL_DEFAULT_INSTALLED_MODULES += $(call build-image-kernel-modules-dir,RECOVERY,$(TARGET_RECOVERY_ROOT_OUT),,modules.load.recovery,,$(dir))) \
  $(eval ALL_DEFAULT_INSTALLED_MODULES += $(call build-image-kernel-modules-dir,VENDOR_RAMDISK,$(TARGET_VENDOR_RAMDISK_OUT),,modules.load,$(VENDOR_RAMDISK_STRIPPED_MODULE_STAGING_DIR),$(dir))) \
  $(eval ALL_DEFAULT_INSTALLED_MODULES += $(call build-vendor-ramdisk-recovery-load,$(dir))) \
  $(eval ALL_DEFAULT_INSTALLED_MODULES += $(call build-image-kernel-modules-dir,VENDOR,$(TARGET_OUT_VENDOR),vendor,modules.load,$(VENDOR_STRIPPED_MODULE_STAGING_DIR),$(dir))) \
  $(eval ALL_DEFAULT_INSTALLED_MODULES += $(call build-image-kernel-modules-dir,ODM,$(TARGET_OUT_ODM),odm,modules.load,,$(dir))) \
  $(if $(filter true,$(BOARD_USES_RECOVERY_AS_BOOT)),\
    $(eval ALL_DEFAULT_INSTALLED_MODULES += $(call build-recovery-as-boot-load,$(dir))),\
    $(eval ALL_DEFAULT_INSTALLED_MODULES += $(call build-image-kernel-modules-dir,GENERIC_RAMDISK,$(TARGET_RAMDISK_OUT),,modules.load,,$(dir)))))
```
- GKI customization
```
BOARD_KERNEL_MODULE_DIRS := 5.4-gki
```
- TARGET_OUT_INTERMEDIATES
- in envsetup.mk
- path of objects
```
TARGET_OUT_INTERMEDIATES := $(PRODUCT_OUT)/obj
```

# Kernel General Definition
---
## TARGET_KERNEL_VERSION
- Zeta: 5.4
```
# define flag to determine the kernel
TARGET_KERNEL_VERSION ?= $(shell ls kernel | grep "msm-*" | sed 's/msm-//')
```
## TARGET_KERNEL
- name and version string of kernel
- Zeta: msm-5.4
```
TARGET_KERNEL := msm-$(TARGET_KERNEL_VERSION)
```
## KERNEL_OUT
- **OBJ** out of kernel but not source out
- .../obj/kernel/msm-5.4
- **path** but NOT a makefile target
```
KERNEL_OUT := $(TARGET_OUT_INTERMEDIATES)/kernel/$(TARGET_KERNEL)
```
- log out
```
KERNEL_OUT : out/target/product/oemc1/obj/kernel/msm-5.4
MSGKI_KERNEL_OUT : out/target/product/oemc1/obj/kernel-gki/msm-5.4
```

## BOARD_KERNEL_BINARIES
- names of kernel binary out
```
# QGKI user build
BOARD_KERNEL_BINARIES := kernel kernel-gki
# QGKI
BOARD_KERNEL_BINARIES := kernel
```

## INSTALLED_KERNEL_TARGET
- This is a make file target.
- qgki + gki target
  - kernel kernel-gki
```
INSTALLED_KERNEL_TARGET := $(foreach k,$(BOARD_KERNEL_BINARIES), $(PRODUCT_OUT)/$(k))
```
- qgki kernel
```
INSTALLED_KERNEL_TARGET := $(PRODUCT_OUT)/kernel
$(INSTALLED_KERNEL_TARGET): $(TARGET_PREBUILT_KERNEL) $(GKI_TARGET_PREBUILT_KERNEL) $(KERNEL_USR_TS)
    cp $(TARGET_PREBUILT_KERNEL) $(PRODUCT_OUT)/kernel; 
```
- gki kernel
```
INSTALLED_KERNEL_TARGET := $(PRODUCT_OUT)/kernel-gki
$(INSTALLED_KERNEL_TARGET): $(TARGET_PREBUILT_KERNEL) $(GKI_TARGET_PREBUILT_KERNEL) $(KERNEL_USR_TS)
    cp $(TARGET_PREBUILT_KERNEL) $(PRODUCT_OUT)/kernel-gki;
```

## TARGET_PREBUILT_INT_KERNEL
- Image.gz, zImage or Image
```
ifeq ($(TARGET_USES_UNCOMPRESSED_KERNEL),)
ifeq ($(KERNEL_ARCH),arm64)
TARGET_PREBUILT_INT_KERNEL := $(KERNEL_OUT)/arch/$(KERNEL_ARCH)/boot/Image.gz
else
TARGET_PREBUILT_INT_KERNEL := $(KERNEL_OUT)/arch/$(KERNEL_ARCH)/boot/zImage
endif
else
$(info Using uncompressed kernel)
TARGET_PREBUILT_INT_KERNEL := $(KERNEL_OUT)/arch/$(KERNEL_ARCH)/boot/Image
endif
```
- log
```
TARGET_PREBUILT_INT_KERNEL : out/target/product/oemc1/obj/kernel-gki/msm-5.4/arch/arm64/boot/Image
```

## TARGET_PREBUILT_KERNEL
- definition
```
TARGET_PREBUILT_KERNEL := $(TARGET_PREBUILT_INT_KERNEL)
$(BOARD_VENDOR_RAMDISK_KERNEL_MODULES): $(TARGET_PREBUILT_KERNEL)
```
- log
```
TARGET_PREBUILT_KERNEL : out/target/product/oemc1/obj/kernel-gki/msm-5.4/arch/arm64/boot/Image
```

## KERNEL_MODULES_INSTALL
- Dynamically-loadable kernel modules (DLKM)
```
KERNEL_MODULES_INSTALL := dlkm
```

## KERNEL_MODULES_OUT
- This definition is a path but NOT a target.
- Kernel modules install path
```
KERNEL_MODULES_OUT := out/target/product/$(PRODUCT_NAME)/$(KERNEL_MODULES_INSTALL)/lib/modules
```
- GKI customization
```
KERNEL_MODULES_OUT := out/target/product/$(PRODUCT_NAME)/$(KERNEL_MODULES_INSTALL)/lib/modules/gki
```
- log
```
KERNEL_MODULES_OUT : out/target/product/oemc1/dlkm/lib/modules/
MSGKI_KERNEL_MODULES_OUT : out/target/product/oemc1/dlkm/lib/modules/gki
```

# MS GKI Specified
---
## MSGKI_BUILD
```
# user qgki + gki build
MSGKI_BUILD := 1
```
## MSGKI_BUILT_ONLY
```
# gki build only
MSGKI_BUILT_ONLY := 1
```

# For vendor.img
---

## BOARD_VENDOR_KERNEL_MODULES
- https://source.android.com/devices/architecture/kernel/loadable-kernel-modules
- In BoardConfig.mk, the Android build defines a BOARD_VENDOR_KERNEL_MODULES variable that provides a full list of the kernel modules intended for the **vendor image**.
- GKI customization
  - BOARD_VENDOR_KERNEL_MODULES_5.4-gki

## VENDOR_KERNEL_MODULES_ARCHIVE
- The **archive-name** of the DLKMs that goes into vendor.img
```
VENDOR_KERNEL_MODULES_ARCHIVE := vendor_modules.zip
```

## BOARD_VENDOR_KERNEL_MODULES_ARCHIVE
- The **archive-pathname** of the DLKMs that goes into vendor.img
```
BOARD_VENDOR_KERNEL_MODULES_ARCHIVE := $(KERNEL_MODULES_OUT)/$(VENDOR_KERNEL_MODULES_ARCHIVE)
```


# For vendor_boot.img
---
## TARGET_VENDOR_RAMDISK_OUT
- TARGET_VENDOR_RAMDISK_OUT - out/target/product/oemc1/vendor-ramdisk
```
  $(eval ALL_DEFAULT_INSTALLED_MODULES += $(call build-image-kernel-modules-dir,VENDOR_RAMDISK,$(TARGET_VENDOR_RAMDISK_OUT),,modules.load,$(VENDOR_RAMDISK_STRIPPED_MODULE_STAGING_DIR),$(dir)))
```

