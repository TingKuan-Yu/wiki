# BOOT.MXF.1.0/boot_images/boot/QcomPkg/SocPkg/Lahaina/LAA/Core.dsc
---
## !include QcomPkg/SocPkg/Lahaina/Common/Core.dsc.inc
- !include - https://edk2-docs.gitbook.io/edk-ii-dsc-specification/3_edk_ii_dsc_file_format/33_platform_dsc_definition#3-3-4-include-statements
  - This section defines the !include statement in EDK II Platform (DSC) files. This statement is used to include, at the statement's line, a file which is processed at that point, **as though the text of the included file was actually in the DSC file.** The included file's content must match the content of the section that the !include statement resides, or it may contain completely new sections. If the included file starts with a section header, then the section being processed in the Platform DSC file is considered to have been terminated.


# BOOT.MXF.1.0/boot_images/boot/QcomPkg/SocPkg/Lahaina/Common/Core.dsc.inc
---
## [PcdsFixedAtBuild.common]
- MsManufacturingModeLib Runtime Variable Attribute PCD
```
  gMsSurfaceCorePkgTokenSpaceGuid.PcdCurrentMfgRuntimeModeVariableAttr|0x00000003 #(EFI_VARIABLE_NON_VOLATILE | EFI_VARIABLE_BOOTSERVICE_ACCESS) = 0x00000003
```
- Zeta EKU
```
  # Zeta Product ID: 68
  gMsSurfaceCorePkgTokenSpaceGuid.PcdMfgModeRequiredEKU|"1.3.6.1.4.1.311.76.9.14.68"
  gMsSurfaceCorePkgTokenSpaceGuid.PcdPkRequiredEKU|"1.3.6.1.4.1.311.76.9.14.68"
  gMsSurfaceCorePkgTokenSpaceGuid.PcdTestMfgModeRequiredEKU|"1.3.6.1.4.1.311.76.9.17"
  gMsSurfaceCorePkgTokenSpaceGuid.PcdTkRequiredEKU|"1.3.6.1.4.1.311.76.9.17"
```

## [Components.common]
- The [Components.common] declares the required inf files
  - common --> for all architecture
  - The Components sections contain lists of EDK II Modules.
    - A module is a compiling unit, which is set by inf file.
  - There are four modules for MFG mode implementation in XBL
    - MsManufacturingMode.inf, MsManufacturingModeDxeLib.inf, MsManufacturingModeUtilitiesDxeLib.inf and MsPlatformManufacturingModeLib.inf
- MS MsManufacturingModeDxe Driver
```
  Sm8350FamilyPkg/Drivers/MsManufacturingModeDxe/MsManufacturingMode.inf
```
- MS MsManufacturingModeDxeLib Library Driver
```
  Sm8350FamilyPkg/Library/MsManufacturingModeDxeLib/MsManufacturingModeDxeLib.inf
```
- MS MsManufacturingModeUtilitiesDxeLib Library Driver
```
  Sm8350FamilyPkg/Library/MsManufacturingModeUtilitiesDxeLib/MsManufacturingModeUtilitiesDxeLib.inf
```
- MS MsPlatformManufacturingModeLib Library Driver
```
  Sm8350FamilyPkg/Library/MsPlatformManufacturingModeLibNull/MsPlatformManufacturingModeLib.inf
```

# BOOT.MXF.1.0/boot_images/boot/Sm8350FamilyPkg/Sm8350FamilyPkg.dec
---
## BOOT.MXF.1.0/boot_images/boot/Sm8350FamilyPkg
- All MsManufacturingMode.inf, MsManufacturingModeDxeLib.inf, MsManufacturingModeUtilitiesDxeLib.inf and MsPlatformManufacturingModeLib.inf are in this directory.
  - It means that MFG mode source codes belong to this Sm8350FamilyPkg package.
- This directory is managed by Sm8350FamilyPkg.dec file.

## [Defines]
- Package name is Sm8350FamilyPkg.
```
  PACKAGE_NAME                   = Sm8350FamilyPkg
```

## [Guids]
- Microsoft Surface Manufacturing Mode Guid
  - GUID for gRT->SetVariable() and gRT->GetVariable()
```
gMsSurfaceManufacturingModeGuid = {0x3811BE0C, 0x6AEF, 0x44DD, {0x93, 0x82, 0xCD, 0x99, 0xA2, 0x4C, 0x66, 0x19 }}
```
- Microsoft Mfg Mode Change Reset Guid
  - GUID for reset function
  - cold reset call - ResetSystemWithSubtype (EfiResetCold, &gMsMfgModeChangeResetGuid);
```
  gMsMfgModeChangeResetGuid = {0x71ab4477, 0x6f9e, 0x46a3, {0x8f, 0x20, 0xe7, 0x64, 0x76, 0x8a, 0x60, 0x2e }}
```

## [PcdsFixedAtBuild] - PcdUefiVersionNumber
- for version comparsion
- refer to BOOT.MXF.1.0/boot_images/boot/Sm8350FamilyPkg/Drivers/MsEnvDxe/MsEnvDxe.c
- The source code in Sm8350FamilyPkg.dec
```
  # 1. Microsoft Uefi Version Number
  gMsSurfaceCorePkgTokenSpaceGuid.PcdUefiVersionNumber|00000000|UINT32|0x40000090
```

## [PcdsFixedAtBuild]
- Override PCD values
  - https://edk2-docs.gitbook.io/edk-ii-dec-specification/3_edk_ii_dec_file_format/310_pcd_sections#summary
  - Each PCD entry must be listed only once per section. If a PCD is listed more than once within one section, the last entry takes precedence.
  - The PCD values in this file are the **default** values. Default values listed in architectural sections **override** default values specified in a 'common' architectural section. 
  - The EDK II build system allows these values may be **overridden** by default values in the **INF** files (provided all INF files use the same default value for PCDs that are used by multiple modules) and by values specified in the **DSC** or **FDF** file. 
  - A PCD's Datum type cannot be changed for different access methods, only one datum type is permitted.

- PcdCurrentMfgRuntimeModeVariableAttr
  - Attribute for SetVariable()
  - default value is **7 =** EFI_VARIABLE_NON_VOLATILE|EFI_VARIABLE_BOOTSERVICE_ACCESS|EFI_VARIABLE_RUNTIME_ACCESS
    - refer to BOOT.MXF.1.0/boot_images/boot/QcomPkg/QcomTestCommon/UefiSim/UefiSim.h
      ```
      /// Attributes of variable.
      #define EFI_VARIABLE_NON_VOLATILE                            0x00000001
      #define EFI_VARIABLE_BOOTSERVICE_ACCESS                      0x00000002
      #define EFI_VARIABLE_RUNTIME_ACCESS                          0x00000004
      ```
    - refer to BOOT.MXF.1.0/boot_images/boot/Sm8350FamilyPkg/Include/Guid/MsSurfaceManufacturingModeVariables.h
      ```
       /**
         Default PCD value equivalent to (EFI_VARIABLE_NON_VOLATILE | EFI_VARIABLE_BOOTSERVICE_ACCESS | 
       EFI_VARIABLE_RUNTIME_ACCESS) = 0x7
       **/
       #define CURRENT_RUNTIME_MODE_VARIABLE_ATTR \
            FixedPcdGet32 (PcdCurrentMfgRuntimeModeVariableAttr)
      ```
```
  # 2. Microsoft Current Mfg Runtime Mode Variable
  gMsSurfaceCorePkgTokenSpaceGuid.PcdCurrentMfgRuntimeModeVariableAttr|0x00000007|UINT32|0x4000001F
```

- EKU default value
```
  ##
  ## This PCD controls the Enhanced Key Usage (EKU) that must be present in the leaf
  ## signer certificate in order to unlock a device.  The default value is 0, which
  ## means "do not require an EKU" in the signature to unlock the device for backwards
  ## compatibility.  Then if the product specific DSC file over-rides this value,
  ## then the verification code will require that the specified EKU is present in the
  ## leaf signer.  This allows us to cut down on the number of Certificate Authorities
  ## (CA's) required, and prevents one product from unlocking another one.  The EKU
  ## for manufacturing mode unlock is 1.3.6.1.4.1.311.76.9.14. or 1.3.6.1.4.1.311.76.9.17.
  ## Assuming the Product ID for a given product is 32, then that product would override
  ## these values with
  ## 1.3.6.1.4.1.311.76.9.14.32
  ## 1.3.6.1.4.1.311.76.9.17.32
  ## 1.3.6.1.4.1.311.76.9.1.32
  ##
  # 3. Microsoft Mfg Mode Required EKU for Production Key
  gMsSurfaceCorePkgTokenSpaceGuid.PcdMfgModeRequiredEKU|"0"|VOID*|0x40000145

  # 4. Microsoft Pk Required EKU for Production Key
  gMsSurfaceCorePkgTokenSpaceGuid.PcdPkRequiredEKU|"0"|VOID*|0x40000146

  # 5. Microsoft Mfg Mode Required EKU for Test Key
  gMsSurfaceCorePkgTokenSpaceGuid.PcdTestMfgModeRequiredEKU|"0"|VOID*|0x40000147

  # 6. Microsoft Pk Required EKU for Test Key
  gMsSurfaceCorePkgTokenSpaceGuid.PcdTkRequiredEKU|"0"|VOID*|0x40000148
```

## [Protocols]
- GUID of Microsoft Mfg Mode Change Notify Protocol
```
  gMsMfgModeChangeNotifyProtocolGuid = { 0xb54d9cd1, 0x3dfb, 0x4c09, { 0xa7, 0x73, 0x2d, 0x46, 0x2d, 0x1d, 0x2e, 0x20 }}
```

# Location of modules
## BOOT.MXF.1.0/boot_images/boot/Sm8350FamilyPkg/Library/MsManufacturingModeDxeLib/
- **MsManufacturingModeDxeLib.inf**
- MsManufacturingModeDxeLib.c

## BOOT.MXF.1.0/boot_images/boot/Sm8350FamilyPkg/Library/MsManufacturingModeUtilitiesDxeLib/
- **MsManufacturingModeUtilitiesDxeLib.inf**
- ManufacturingModeInstructions.txt  
- MsManufacturingModeUtilitiesDxeLib.c  

## BOOT.MXF.1.0/boot_images/boot/Sm8350FamilyPkg/Library/MsPlatformManufacturingModeLibNull
- **MsPlatformManufacturingModeLib.inf**
- MsPlatformManufacturingModeLib.c  

## BOOT.MXF.1.0/boot_images/boot/Sm8350FamilyPkg/Drivers/MsManufacturingModeDxe
- **MsManufacturingMode.inf**
- ManufacturingModeInstructions.txt
  - Instructions for enabling UEFI MANUFACTURING_MODE or CUSTOMER_MODE.
  - Not for user but for driver developer.
- MsManufacturingMode.c

## BOOT.MXF.1.0/boot_images/boot/Sm8350FamilyPkg/Include/Library/
- MsManufacturingModeDxeLib.h  
- MsManufacturingModeUtilitiesDxeLib.h
- MsManufacturingModeLib.h

## BOOT.MXF.1.0/boot_images/boot/Sm8350FamilyPkg/Include/Guid/
- MsSurfaceManufacturingModeVariables.h
  - define definition for MFG mode here
  - Global for driver, utility and other include files
  - example of CURRENT_RUNTIME_MODE_VARIABLE_ATTR
  ```
  /**
    Default PCD value equivalent to (EFI_VARIABLE_NON_VOLATILE | EFI_VARIABLE_BOOTSERVICE_ACCESS | 
    EFI_VARIABLE_RUNTIME_ACCESS) = 0x7
  **/
  #define CURRENT_RUNTIME_MODE_VARIABLE_ATTR \
        FixedPcdGet32 (PcdCurrentMfgRuntimeModeVariableAttr)
  ```

