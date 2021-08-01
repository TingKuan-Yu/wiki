# Flow
---
1. After the chipset is reset, the Qualcomm® Kryo™ CPU Silver core 0 comes out of reset and executes PBL.    On Kryo Silver core 0, application primary boot loader (APPS PBL) initializes hardware (timer, PRNG, clocks, and so on), enables caches and MMU, and detects the boot device as per the boot option  configuration:
▪ Default boot option: UFS > SD > Emergency Download mode (EDL)
▪ Default boot option: **overridden by EDL cookie** or force USB GPIO

2a. APPS PBL loads and authenticates XBL_Loader (region # 1) from the boot device to boot IMEM.

2b. APPS PBL loads and authenticates XBL_SDI (region # 2) from the boot device to OCIMEM.

2c. APPS PBL loads and authenticates XBL_SEC (region # 0) from the boot device to boot IMEM. Jumps to XBL_SEC.

# The XBL_Loader, XBL_SDI and XbL_SEC 
## Overview
---
- These modules are not UEFI modules. They are SBL modules.

# XBL_Loader
---
## XBL_Loader platform description (DSC) file
- BOOT.MXF.1.0/boot_images/boot/QcomPkg/SocPkg/**Lahaina**/Common/Loader.dsc



## XBL_Loader Package
### BOOT.MXF.1.0/boot_images/boot/QcomPkg/XBLLoaderApi.dec
- [Defines]
```
PACKAGE_NAME                   = XBLLoaderApi
```
- [Includes.common]
```
  XBLLoader/Include
  XBLRamDump
  XBLLoader
  SocPkg/Library/XBLLoaderLib
```

### XBL_SDI 

### XbL_SEC 


# XBL_Loader

```
BOOT.MXF.1.0/boot_images/boot/QcomPkg/XBLLoaderApi.dec
BOOT.MXF.1.0/boot_images/boot/QcomPkg/Include/XBLLoader
BOOT.MXF.1.0/boot_images/boot/QcomPkg/XBLLoader
BOOT.MXF.1.0/boot_images/boot/QcomPkg/SocPkg/Lahaina/Settings/SMEM/smem_xbl_loader.xml
BOOT.MXF.1.0/boot_images/boot/QcomPkg/SocPkg/Library/XBLLoaderArchLib
BOOT.MXF.1.0/boot_images/boot/QcomPkg/SocPkg/Library/XBLLoaderLib
BOOT.MXF.1.0/boot_images/boot/QcomPkg/Library/UartQupv3Lib/UartXBLLoaderOs.c
BOOT.MXF.1.0/boot_images/boot/QcomPkg/Library/SmemLib/src/smem_xbl_loader.c
BOOT.MXF.1.0/boot_images/boot/QcomPkg/Library/SmemLib/build/SmemLibXBLLoader.inf
BOOT.MXF.1.0/boot_images/boot/QcomPkg/Library/ChipInfoLib/ChipInfoImage_XBLLoader.c
```
- BOOT.MXF.1.0/boot_images/boot/QcomPkg/XBLLoader/XBLLoader.inf
```
  [Sources.AARCH64]
  ModuleEntryPoint.S
```

# XBL_SDI

# SBL_SEC