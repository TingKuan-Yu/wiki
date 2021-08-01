[[_TOC_]]

# Reference
- https://github.com/tianocore/tianocore.github.io/wiki/EDK-II-Documentation#specifications

# .dsc (platform level) > .inf (file information for compiler)
- .dec file describes the scope of a packages including files and definitions
- .inf can refer to .dec to find files and definitions.

# the buildconfig.json
## json file in XBL
```
BOOT.MXF.1.0/boot_images/boot/QcomPkg/SocPkg/Lahaina/buildconfig.json
BOOT.MXF.1.0/boot_images/boot/QcomPkg/SocPkg/Cedros/buildconfig.json
BOOT.MXF.1.0/boot_images/boot/QcomPkg/SocPkg/Kodiak/buildconfig.json
BOOT.MXF.1.0/boot_images/boot/QcomPkg/QcomToolsPkg/buildconfig.json
BOOT.MXF.1.0/boot_images/boot/QcomPkg/QcomTestPkg/buildconfig.json
```
## Example of Lahaina buildconfig.json 
- The buildconfig.json use **Loader.dsc** file to **XBLLoader.dll**.
- BOOT.MXF.1.0/boot_images/boot/QcomPkg/SocPkg/Lahaina/buildconfig.json
```
                 {
                   "Name" : "XBL_Loader" ,
                   "Process" : [
								 {
                                   "ToolChain" : "dll_path" ,
								   "Params" : ["-t","$BUILDROOT/boot/QcomPkg/Library/DllPathSaveLib","-d", "boot_images/Build/Lahaina$VAR/Dll/$REL/XBLLoader.dll","-m","XBLLoader"]
                                 },
                                 {
                                   "ToolChain" : "VoltagePlanParser" ,
                                   "Params" : ["xbl","8350","QcomPkg/SocPkg/Lahaina/Settings/CPR","QcomPkg/SocPkg/Lahaina/Settings/CPR","QcomPkg/SocPkg/Lahaina/Library/CPRTargetLib/target/8350"]
                                 },
                                 {
                                   "ToolChain" : "CLANG100" ,
                                   "AArch" : "AARCH64" ,
                                   "Params" : ["$EDK2ROOT/BaseTools/Source/Python/build/build.py","-p","QcomPkg/SocPkg/Lahaina/Common/Loader.dsc","--verbose","-j", "QcomPkg/SocPkg/Lahaina/$VAR/build_Loader.log","-w","-a","AARCH64","-b","$REL"]
                                 },
                                 {
                                   "ToolChain" : "Lib_Size_check",
                                   "Params" : ["-m","$BUILDROOT/Build/Lahaina$VAR/Loader/$REL_$COMPILER/$AARCH/QcomPkg/XBLLoader/XBLLoader/DEBUG/XBLLoader_mapit_bootimem_ocimem.txt","-c","$BOOTROOT/QcomPkg/SocPkg/Lahaina/$VAR/libssizecfg.json","-j", "QcomPkg/SocPkg/Lahaina/$VAR/build_Libsizecheck.log"]	
                                 }
                               ]
                 } ,

```

# The .dsc file
- Refer to https://edk2-docs.gitbook.io/edk-ii-dsc-specification/
- The function of the platform DSC file is to specify the library instances, components and output formats used **to generate binary files that will be processed by other tools to generate an image** that is either put into a flash device, made available for recovery booting or updating existing firmware on a platform.
- The platform description (DSC) file
  - The platform DSCs have located in their respective "[Platform Name] **Pkg**" folders.
- EDK II DSC files are a list of:
  - EDK II Module INF Files
  - EDK Components
  - EDK libraries (only used by EDK Components)
  - EDK II Library Class Instance Mappings (only used by EDK II Modules)
  - EDK II PCD Entries
- The dsc file includes inf file

# The .INF file
- This file describes how to build a module (i.e. a driver, library, application, etc…).
- The intent of a component's INF file is to define the source files, libraries (or library classes), and definitions relevant to building the component
- Refer to https://edk2-docs.gitbook.io/edk-ii-inf-specification/

# The .DEC File
- Package Declaration File (DEC)
  - This file declares information about what is provided in the **package**. 
  - https://tianocore-docs.github.io/edk2-DecSpecification/release-1.27/
- An EDK II Package (directory) is a directory that contains an EDK II package declaration (DEC) file.
- This file is used to declare what is available in the package (directory) and tells the build system where to find things such as “**Include**” directories. 
- It can also be used to replace the use of #define values or constant variables in .h files through a mechanism called the Platform Configuration Database(PCD). This file is used when a module includes this package in its [Packages] section.
- The DEC files are used by the EDK II utilities that parse EDK II DSC and EDK II INF files to generate AutoGen.c and AutoGen.h files for the EDK II build infrastructure.

# PCD
- PDC stands for Platform Configuration Database.
- PCDs are declared as part of the DEC, and referenced in a modules INF and a package’s DSC.
- dec:   TokenSpaceGuidCname.PcdCname|DefaultValue|DatumType|Token
- Are all PCDs stored as variables?
  1. PCDs of type FeatureFlag are declared as CONST variables in every module that uses that PCD
  2. PCDs of type FixedAtBuild are also declared as CONST variables in every module that uses that PCD
  3. PCDs if type PatchableInModule are declared as ‘volatile’ variables in every the module that uses that PCD.
  4. PCDs of type Dynamic/DynamicEx are global to the entire platform. There are 3 subtypes of Dynamic/DynamicEx. The first is VPD, which are Read-Only and is stored in an uncompressed section of the system FLASH/ROM. The second is HII, which are R/W and Non-Volatile, and they are mapped to an EFI Variable which is named by a GUID + UnicodeString + ByteOffset. The third is Default, which are R/W and Volatile, which means their contents are lost every time the platform is reset or power cycled.

# The EDK2 FDF dile
- The EDK II Flash Description File (FDF) file specifies how to package the binaries files into UEFI/PI compliant images.

# gBS
  - The global variable for the UEFI Boot Services Table, called gBS
  - https://edk2-docs.gitbook.io/edk-ii-uefi-driver-writer-s-guide/5_uefi_services/51_services_that_uefi_drivers_commonly_use/511_memory_allocation_services

# references
- Build-Description-Files: https://github.com/tianocore/tianocore.github.io/wiki/Build-Description-Files


