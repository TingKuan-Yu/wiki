# Source Tree
```
tingkuanyu@TonyYuLinux1:/E/c2/11/main/abl/abl_working/BOOT.MXF.1.0/boot_images$ tree -L 1
.
├── boot
├── boot_tools
├── edk2
├── sdk
├── sectools
└── ssg
```
## boot
- boot folder contains **Sm8350FamilyPkg**
```
├── boot
│   ├── copyright_check.sh
│   ├── klocwork.bat
│   ├── parser.log
│   ├── QcomPkg
│   ├── Sm8350FamilyPkg
│   ├── toolchainconfig.json
│   ├── UEFI_License_and_Notice_File_QC.txt
│   └── watchit.py
```
## boot_tools
- python scripts for code building
```
├── boot_tools
│   ├── buildabl.py
│   ├── buildex.py
│   ├── build_tools
│   ├── callgraph
│   ├── cmm
│   ├── create_multielf.py
│   ├── create_trdata.py
│   ├── createversionelf.py
│   ├── createxbl.py
│   ├── delcomments.py
│   ├── devcfg
│   ├── esc_backslash.py
│   ├── gcc_map.py
│   ├── genmanifest.py
│   ├── genmelfscript.py
│   ├── image_header.py
│   ├── klocwork
│   ├── LibSizeCheck.py
│   ├── manifest
│   ├── mapparser
│   ├── mbn_tools.py
│   ├── nand_preamble.py
│   ├── packit.py
│   ├── pt_32.py
│   ├── pt_64.py
│   ├── QcomCopyright.py
│   ├── scripts
│   ├── SourceFileCheck.py
│   ├── spy_buildex.py
│   └── XBLConfig
```
- edk2
- includes EDK2 packages which could be used by Sm8350FamilyPkg
```
├── edk2
│   ├── ArmPkg
│   ├── ArmPlatformPkg
│   ├── BaseTools
│   ├── BuildNotes2.txt
│   ├── Conf
│   ├── CryptoPkg
│   ├── dll_path_list
│   ├── Edk2Setup.bat
│   ├── edksetup.bat
│   ├── edksetup.sh
│   ├── EmbeddedPkg
│   ├── FatPkg
│   ├── FmpDevicePkg
│   ├── Maintainers.txt
│   ├── MdeModulePkg
│   ├── MdePkg
│   ├── NetworkPkg
│   ├── OptionRomPkg
│   ├── SecurityPkg
│   └── ShellPkg
```
## sdk
```
├── sdk
│   ├── BaseTools_SDK
│   ├── QcomSdkPkg
│   ├── QcomSdkPkgRelease.inf
│   └── quantum_sdk_build.py
```
## sectools
```
├── sectools
│   ├── bin
│   ├── config
│   ├── example
│   ├── ext
│   ├── NOTICE
│   ├── pack
│   ├── plugin
│   ├── resources
│   ├── sectools
│   ├── sectools_builder.py
│   ├── Sectools.inf
│   └── sectools.py
```
# ssg packages
```
└── ssg
    ├── SecPkg
    └── xbl_sec

```
