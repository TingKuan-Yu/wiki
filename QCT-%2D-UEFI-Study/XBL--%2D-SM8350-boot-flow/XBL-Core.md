# USER_DEFINED Module
---
## https://edk2buildsystem.gitbooks.io/fdf_spec/content/12_terms.html
- The EDK II build system also permits modules of type USER_DEFINED. These modules will not be processed by the EDK II Build system.
  - Module Type
    All libraries and components belong to one of the following module types: BASE, SEC, PEI_CORE, PEIM, SMM_CORE, DXE_CORE, DXE_DRIVER, DXE_RUNTIME_DRIVER, DXE_SMM_DRIVER, DXE_SAL_DRIVER, UEFI_DRIVER, or UEFI_APPLICATION. These definitions provide a framework that is consistent with a similar set of requirements. A module that is of module type BASE, depends only on headers and libraries provided in the MDE, while a module that is of module type DXE_DRIVER depends on common DXE components. For a definition of the various module types, see module type. The EDK II build system also permits modules of type USER_DEFINED. These modules will not be processed by the EDK II Build system.

## https://edk2-docs.gitbook.io/edk-ii-inf-specification/appendix_f_module_types


# BOOT.MXF.1.0/boot_images/boot/QcomPkg/XBLLoader/XBLLoader.inf
---
## reference 
- https://edk2-docs.gitbook.io/edk-ii-inf-specification/2_inf_overview

## [Defines]
- USER_DEFINED module type. XBLLoader is not a UEFI module. However, it uses the UEFI building system for compiling code.
- Possible values for MODULE_TYPE, and their descriptions, are listed in the table, "EDK II Module Types." For each module, the BASE_NAME and MODULE_TYPE are required. The BASE_NAME definition is case sensitive as it will be used to create a directory name **during a build**.
  - https://edk2-docs.gitbook.io/edk-ii-inf-specification/3_edk_ii_inf_file_format/34_-defines-_section#summary
- source
```
  BASE_NAME                      = XBLLoader
  MODULE_TYPE                    = USER_DEFINED
```

## [Sources.common]
- c source code
```
  boot_gpt_partition_id.c
```

## [Sources.AARCH64]
- assembly source code
```
  ModuleEntryPoint.S
```

## [LibraryClasses]
- Refer to https://edk2-docs.gitbook.io/edk-ii-module-writer-s-guide/3_module_development/37_building_the_module#3-7-2-select-library-instances
- For drivers and applications, a library instance for each library class dependency must be selected and **linked** to its binary EFI image.
- Notice: XblHlosHobLib is used in used in XBLLoader
- source
```
  ConfigContextLib
:
  ExtFGLib  # MSCHANGE MSE Charging Library
  MSEChgHW # MSCHANGE
  XblHlosHobLib  # MSCHANGE enabling MS charging libraries
```

## Built Objects
```
BOOT.MXF.1.0/boot_images/Build/LahainaLAA/Loader/RELEASE_CLANG100LINUX/AARCH64/XBLLoader.ld
BOOT.MXF.1.0/boot_images/Build/LahainaLAA/Loader/RELEASE_CLANG100LINUX/AARCH64/QcomPkg/XBLLoader/XBLLoader/OUTPUT/XBLLoader.inf
BOOT.MXF.1.0/boot_images/Build/LahainaLAA/Loader/RELEASE_CLANG100LINUX/AARCH64/QcomPkg/XBLLoader/XBLLoader/OUTPUT/XBLLoader.lib
BOOT.MXF.1.0/boot_images/Build/LahainaLAA/Loader/RELEASE_CLANG100LINUX/AARCH64/QcomPkg/XBLLoader/XBLLoader/XBLLoader.makefile
BOOT.MXF.1.0/boot_images/Build/LahainaLAA/Loader/RELEASE_CLANG100LINUX/AARCH64/QcomPkg/XBLLoader/XBLLoader/DEBUG/XBLLoader.map
BOOT.MXF.1.0/boot_images/Build/LahainaLAA/Loader/RELEASE_CLANG100LINUX/AARCH64/QcomPkg/XBLLoader/XBLLoader/DEBUG/XBLLoader.dll

BOOT.MXF.1.0/boot_images/Build/LahainaLAA/Dll/RELEASE/XBLLoader.dll
```






