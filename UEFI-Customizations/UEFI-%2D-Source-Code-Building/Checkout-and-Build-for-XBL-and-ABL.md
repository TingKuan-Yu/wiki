[[_TOC_]]

#**XBL** 

**Repo**

New: ADO -> device, BOOT.MXF.1.0-premium-high-2020-spf-1-0_amss_standard_oem 

Old: ADO -> device, qcom-BOOT.MXF.1.0-premium-high-2020-spf-1-0_amss_standard_oem 

Checkout 
```
repo init -u ssh://ssh.dev.azure.com/v3/e-os/device/manifest -b c1/11/main -m nhlos/boot.xml 

repo sync –j 8 
```

**Build** 
```

./build.sh build_boot 
```

Result 

BOOT.MXF.1.0/boot_image/boot/QcomPkg/SocPkg/Lahaina/Bin/LAA/RELEASE/ 

xbl.elf, xbl_config.elf, and shrm.elf 

**Clean** 
```

./build.sh clean_boot 
```

**Remove** 
```
rm -rf BOOT.MXF.1.0/boot_images/Build/ 

rm -rf BOOT.MXF.1.0/boot_images/boot/QcomPkg/SocPkg/Lahaina/Bin/LAA/RELEASE or DEBUG 
```
 

#ABL 

**Repo**

New: ADO -> device, priv-la.9.14-abl.tianocore.edk2 

Old: ADO -> private-device, abl.tianocore.edk2 

**Checkout** 

Under NHLOS: 
```

repo init -u ssh://ssh.dev.azure.com/v3/e-os/device/manifest -b c1/11/main -m nhlos/abl.xml 

repo sync –j 8 
```

Under Vendor: 
```

repo init -u ssh://ssh.dev.azure.com/v3/e-os/device/manifest -b c1/11/main -m vendor.xml 

repo sync -c --no-tags --no-clone-bundle -j 8 
```

**Build** 

Under NHLOS: 
```
./build.sh build_abl 
```

Under Vendor: 
```

eos_build/scripts/build.sh -env 

source build/envsetup.sh && lunch oemc1-userdebug && make -j8 aboot 
```

**Result** 

Bootable/bootloader/edk2/QcomModulePkg/Bin/RELEASE 

abl.elf 

**Clean** 
```
./build.sh clean_abl 
```

 