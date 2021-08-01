INTERNAL_VENDOR_RAMDISK_FILES := $(filter $(TARGET_VENDOR_RAMDISK_OUT)/%, \
    $(ALL_GENERATED_SOURCES) \
    $(ALL_DEFAULT_INSTALLED_MODULES))
```
INTERNAL_VENDOR_RAMDISK_FILES = 
out/target/product/oemc1/vendor-ramdisk/first_stage_ramdisk/fstab.default 
out/target/product/oemc1/vendor-ramdisk/first_stage_ramdisk/fstab.emmc 
out/target/product/oemc1/vendor-ramdisk/lib/modules/modules.dep 
out/target/product/oemc1/vendor-ramdisk/lib/modules/modules.alias 
out/target/product/oemc1/vendor-ramdisk/lib/modules/modules.softdep 
out/target/product/oemc1/vendor-ramdisk/lib/modules/modules.load
```

#  build-image-kernel-modules-depmod
- build script
```
define build-image-kernel-modules-depmod
$(3)/$(DEPMOD_STAGING_SUBDIR)/modules.dep: .KATI_IMPLICIT_OUTPUTS := $(3)/$(DEPMOD_STAGING_SUBDIR)/modules.alias $(3)/$(DEPMOD_STAGING_SUBDIR)/modules.softdep $(3)/$(DEPMOD_STAGING_SUBDIR)/$(5)
$(3)/$(DEPMOD_STAGING_SUBDIR)/modules.dep: $(DEPMOD)
$(3)/$(DEPMOD_STAGING_SUBDIR)/modules.dep: PRIVATE_MODULES := $(1)
$(3)/$(DEPMOD_STAGING_SUBDIR)/modules.dep: PRIVATE_MOUNT_POINT := $(2)
$(3)/$(DEPMOD_STAGING_SUBDIR)/modules.dep: PRIVATE_MODULE_DIR := $(3)/$(DEPMOD_STAGING_SUBDIR)/$(2)/lib/modules/$(8)
$(3)/$(DEPMOD_STAGING_SUBDIR)/modules.dep: PRIVATE_STAGING_DIR := $(3)
$(3)/$(DEPMOD_STAGING_SUBDIR)/modules.dep: PRIVATE_LOAD_MODULES := $(4)
$(3)/$(DEPMOD_STAGING_SUBDIR)/modules.dep: PRIVATE_LOAD_FILE := $(3)/$(DEPMOD_STAGING_SUBDIR)/$(5)
$(3)/$(DEPMOD_STAGING_SUBDIR)/modules.dep: PRIVATE_MODULE_ARCHIVE := $(6)
$(3)/$(DEPMOD_STAGING_SUBDIR)/modules.dep: PRIVATE_OUTPUT_DIR := $(7)
$(3)/$(DEPMOD_STAGING_SUBDIR)/modules.dep: $(1) $(6)
	@echo depmod $$(PRIVATE_STAGING_DIR)
	rm -rf $$(PRIVATE_STAGING_DIR)
	mkdir -p $$(PRIVATE_MODULE_DIR)
	$(if $(6),\
	  unzip -qoDD -d $$(PRIVATE_MODULE_DIR) $$(PRIVATE_MODULE_ARCHIVE); \
	  mkdir -p $$(PRIVATE_OUTPUT_DIR)/lib; \
	  cp -r  $(3)/$(DEPMOD_STAGING_SUBDIR)/$(2)/lib/modules $$(PRIVATE_OUTPUT_DIR)/lib/; \
	  find $$(PRIVATE_MODULE_DIR) -type f -name *.ko | xargs basename -a > $$(PRIVATE_LOAD_FILE); \
	)
	$(if $(1),\
	  cp $$(PRIVATE_MODULES) $$(PRIVATE_MODULE_DIR)/; \
	  for MODULE in $$(PRIVATE_LOAD_MODULES); do \
	    basename $$$$MODULE >> $$(PRIVATE_LOAD_FILE); \
	  done; \
	)
	$(DEPMOD) -b $$(PRIVATE_STAGING_DIR) 0.0
	# Turn paths in modules.dep into absolute paths
	sed -i.tmp -e 's|\([^: ]*lib/modules/[^: ]*\)|/\1|g' $$(PRIVATE_STAGING_DIR)/$$(DEPMOD_STAGING_SUBDIR)/modules.dep
	touch $$(PRIVATE_LOAD_FILE)
endef
```
- log out
```
/E/GKI/hlos_vendor/out/build-oemc1.ninja:375547:  command = /bin/bash -c "(rm -rf out/target/product/oemc1/obj/PACKAGING/depmod_VENDOR_RAMDISK_intermediates ) && (mkdir -p out/target/product/oemc1/obj/PACKAGING/depmod_VENDOR_RAMDISK_intermediates/lib/modules/0.0//lib/modules/ ) && (unzip -qoDD -d out/target/product/oemc1/obj/PACKAGING/depmod_VENDOR_RAMDISK_intermediates/lib/modules/0.0//lib/modules/ out/target/product/oemc1/dlkm/lib/modules/vendor_ramdisk_modules.zip; mkdir -p out/target/product/oemc1/vendor-ramdisk/lib; cp -r  out/target/product/oemc1/obj/PACKAGING/depmod_VENDOR_RAMDISK_intermediates/lib/modules/0.0//lib/modules out/target/product/oemc1/vendor-ramdisk/lib/; find out/target/product/oemc1/obj/PACKAGING/depmod_VENDOR_RAMDISK_intermediates/lib/modules/0.0//lib/modules/ -type f -name *.ko | xargs basename -a > out/target/product/oemc1/obj/PACKAGING/depmod_VENDOR_RAMDISK_intermediates/lib/modules/0.0/modules.load ) && (out/host/linux-x86/bin/depmod -b out/target/product/oemc1/obj/PACKAGING/depmod_VENDOR_RAMDISK_intermediates 0.0 ) && (sed -i.tmp -e 's|\\([^: ]*lib/modules/[^: ]*\\)|/\\1|g' out/target/product/oemc1/obj/PACKAGING/depmod_VENDOR_RAMDISK_intermediates/lib/modules/0.0/modules.dep ) && (touch out/target/product/oemc1/obj/PACKAGING/depmod_VENDOR_RAMDISK_intermediates/lib/modules/0.0/modules.load )"
```

- test
```
find out/target/product/oemc1/vendor-ramdisk/lib/modules/ -type f -name *.ko | xargs basename -a
find out/target/product/oemc1/vendor-ramdisk/lib/modules/ -type f -name *.ko | xargs basename -a| sort -n
find modules/unstripped/ -printf "%AY%Am%Ad%AH%AM%AS %p\n" | sort -n | awk '{ print $2 }'  | xargs basename -a
```
```
find /path -printf "%AY%Am%Ad%AH%AM%AS %p\n" | sort -n
echo "$$(VENDOR_RAMDISK_KERNEL_MODULES)" | tr " " "\n" > $$(PRIVATE_LOAD_FILE); \"
```