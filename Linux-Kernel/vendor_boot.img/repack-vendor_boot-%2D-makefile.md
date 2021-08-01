# unpack vendor_boot
[extract-vendor_boot.sh.tar.gz](/.attachments/extract-vendor_boot.sh.tar-188ecf7b-8716-451b-bd62-848654943e81.gz)
```
#!/bin/bash

rm -f ramdisk
rm -f ramdisksize

CURRENT_VENDOR_BOOT=vendor_boot.img

dd if=${CURRENT_VENDOR_BOOT} of=ramdisksize bs=1 skip=24 count=4
RAMDISK_SIZE=$(od -N4 -t u4 ramdisksize | awk 'NR==1{ print $2}')
echo "RAMDISK_SIZE: ${RAMDISK_SIZE}"
cala=`expr ${RAMDISK_SIZE} + 4095`
calb=`expr ${cala} / 4096`
echo "calb: ${calb}"
dd if=${CURRENT_VENDOR_BOOT} of=ramdisk.gz skip=1 bs=4096 count=${calb}
gunzip -c ramdisk.gz > ramdisk
rm -rf extract && mkdir extract && pushd extract/ && cat ../ramdisk | cpio -idmv

```

# vendor boot image
---
## pre-check
```
ifeq ($(BUILDING_VENDOR_BOOT_IMAGE),true)

ifeq ($(PRODUCT_SUPPORTS_VERITY),true)
  $(error vboot 1.0 does not support vendor_boot partition)
endif
```

## make ramdisk cpio
```
INTERNAL_VENDOR_RAMDISK_FILES := $(filter $(TARGET_VENDOR_RAMDISK_OUT)/%, \
    $(ALL_GENERATED_SOURCES) \
    $(ALL_DEFAULT_INSTALLED_MODULES))

INTERNAL_VENDOR_RAMDISK_TARGET := $(call intermediates-dir-for,PACKAGING,vendor-boot)/vendor-ramdisk.cpio.gz
$(INTERNAL_VENDOR_RAMDISK_TARGET): $(MKBOOTFS) $(INTERNAL_VENDOR_RAMDISK_FILES) | $(COMPRESSION_COMMAND_DEPS)
	$(MKBOOTFS) -d $(TARGET_OUT) $(TARGET_VENDOR_RAMDISK_OUT) | $(COMPRESSION_COMMAND) > $@
```
- print log
```
MKBOOTFS = out/host/linux-x86/bin/mkbootfs
INTERNAL_VENDOR_RAMDISK_FILES = out/target/product/oemc1/vendor-ramdisk/first_stage_ramdisk/fstab.default out/target/product/oemc1/vendor-ramdisk/first_stage_ramdisk/fstab.emmc out/target/product/oemc1/vendor-ramdisk/lib/modules/modules.dep out/target/product/oemc1/vendor-ramdisk/lib/modules/modules.alias out/target/product/oemc1/vendor-ramdisk/lib/modules/modules.softdep out/target/product/oemc1/vendor-ramdisk/lib/modules/modules.load
COMPRESSION_COMMAND_DEPS = out/host/linux-x86/bin/minigzip
TARGET_OUT = out/target/product/oemc1/system
TARGET_VENDOR_RAMDISK_OUT = out/target/product/oemc1/vendor-ramdisk
COMPRESSION_COMMAND = out/host/linux-x86/bin/minigzip
``
## parameters
```
ifdef BOARD_INCLUDE_DTB_IN_BOOTIMG
  INTERNAL_VENDOR_BOOTIMAGE_ARGS += --dtb $(INSTALLED_DTBIMAGE_TARGET)
endif
ifdef BOARD_KERNEL_BASE
  INTERNAL_VENDOR_BOOTIMAGE_ARGS += --base $(BOARD_KERNEL_BASE)
endif
ifdef BOARD_KERNEL_PAGESIZE
  INTERNAL_VENDOR_BOOTIMAGE_ARGS += --pagesize $(BOARD_KERNEL_PAGESIZE)
endif
ifdef INTERNAL_KERNEL_CMDLINE
  INTERNAL_VENDOR_BOOTIMAGE_ARGS += --vendor_cmdline "$(INTERNAL_KERNEL_CMDLINE)"
endif
```
## target
```
INSTALLED_VENDOR_BOOTIMAGE_TARGET := $(PRODUCT_OUT)/vendor_boot.img
$(INSTALLED_VENDOR_BOOTIMAGE_TARGET): $(MKBOOTIMG) $(INTERNAL_VENDOR_RAMDISK_TARGET) $(INSTALLED_DTBIMAGE_TARGET)
```
## print parameter info
```
$(info INSTALLED_VENDOR_BOOTIMAGE_TARGET = $(INSTALLED_VENDOR_BOOTIMAGE_TARGET))
$(info MKBOOTIMG = $(MKBOOTIMG))
$(info INTERNAL_VENDOR_RAMDISK_TARGET = $(INTERNAL_VENDOR_RAMDISK_TARGET))
$(info INSTALLED_DTBIMAGE_TARGET = $(INSTALLED_DTBIMAGE_TARGET))
$(info BOARD_AVB_ENABLE = $(BOARD_AVB_ENABLE))
$(info BOARD_AVB_VENDOR_BOOTIMAGE_KEY_PATH = $(BOARD_AVB_VENDOR_BOOTIMAGE_KEY_PATH))
$(info INTERNAL_VENDOR_BOOTIMAGE_ARGS = $(INTERNAL_VENDOR_BOOTIMAGE_ARGS))
$(info INTERNAL_MKBOOTIMG_VERSION_ARGS = $(INTERNAL_MKBOOTIMG_VERSION_ARGS))
$(info BOARD_MKBOOTIMG_ARGS = $(BOARD_MKBOOTIMG_ARGS))

```
- result
  - print
    ```
    INSTALLED_VENDOR_BOOTIMAGE_TARGET = out/target/product/oemc1/vendor_boot.img

    MKBOOTIMG = out/host/linux-x86/bin/mkbootimg

    INTERNAL_VENDOR_RAMDISK_TARGET = out/target/product/oemc1/obj/PACKAGING/vendor- 
    boot_intermediates/vendor-ramdisk.cpio.gz

    INSTALLED_DTBIMAGE_TARGET = out/target/product/oemc1/dtb.img

    BOARD_AVB_ENABLE = true

    BOARD_AVB_VENDOR_BOOTIMAGE_KEY_PATH = 

    INTERNAL_VENDOR_BOOTIMAGE_ARGS = --dtb out/target/product/oemc1/dtb.img --base 0x00000000 --pagesize 
    4096 --vendor_cmdline "console=ttyMSM0,115200n8 androidboot.console=ttyMSM0 androidboot.memcg=1 
    lpm_levels.sleep_disabled=1 video=vfb:640x400,bpp=32,memsize=3072000 msm_rtb.filter=0x237 
    service_locator.enable=1 androidboot.usbcontroller=a600000.dwc3 swiotlb=0 loop.max_part=7 
    cgroup.memory=nokmem,nosocket pcie_ports=compat iptable_raw.raw_before_defrag=1 
    ip6table_raw.raw_before_defrag=1 androidboot.hardware=oemc1 androidboot.hardware.platform=qcom 
    buildvariant=user"

    INTERNAL_MKBOOTIMG_VERSION_ARGS = --os_version 11 --os_patch_level 2021-03-05

    BOARD_MKBOOTIMG_ARGS = --header_version 3
    ```

- build scripts

```
ifeq ($(BOARD_AVB_ENABLE),true)
$(INSTALLED_VENDOR_BOOTIMAGE_TARGET): $(AVBTOOL) $(BOARD_AVB_VENDOR_BOOTIMAGE_KEY_PATH)
	$(call pretty,"Target vendor_boot image: $@")
	$(MKBOOTIMG) $(INTERNAL_VENDOR_BOOTIMAGE_ARGS) $(INTERNAL_MKBOOTIMG_VERSION_ARGS) $(BOARD_MKBOOTIMG_ARGS) --vendor_ramdisk $(INTERNAL_VENDOR_RAMDISK_TARGET) --vendor_boot $@
	$(call assert-max-image-size,$@,$(BOARD_VENDOR_BOOTIMAGE_PARTITION_SIZE))
	$(AVBTOOL) add_hash_footer \
           --image $@ \
	   --partition_size $(BOARD_VENDOR_BOOTIMAGE_PARTITION_SIZE) \
	   --partition_name vendor_boot $(INTERNAL_AVB_VENDOR_BOOT_SIGNING_ARGS) \
	   $(BOARD_AVB_VENDOR_BOOT_ADD_HASH_FOOTER_ARGS)
else
$(INSTALLED_VENDOR_BOOTIMAGE_TARGET):
	$(call pretty,"Target vendor_boot image: $@")
	$(MKBOOTIMG) $(INTERNAL_VENDOR_BOOTIMAGE_ARGS) $(INTERNAL_MKBOOTIMG_VERSION_ARGS) $(BOARD_MKBOOTIMG_ARGS) --vendor_ramdisk $(INTERNAL_VENDOR_RAMDISK_TARGET) --vendor_boot $@
	$(call assert-max-image-size,$@,$(BOARD_VENDOR_BOOTIMAGE_PARTITION_SIZE))
endif
endif # BUILDING_VENDOR_BOOT_IMAGE
```