== under construction ==

# BOOT.MXF.1.0/boot_images/boot/Sm8350FamilyPkg/Library/MsManufacturingModeDxeLib/
## MsManufacturingModeDxeLib.inf
- [Defines]
  - BASE_NAME                      = MsManufacturingModeDxeLib
    - BOOT.MXF.1.0/boot_images/Build/LahainaLAA/Core/RELEASE_CLANG100LINUX/AARCH64/Sm8350FamilyPkg/Library/MsManufacturingModeDxeLib/MsManufacturingModeDxeLib/OUTPUT/MsManufacturingModeDxeLib.lib
    - BOOT.MXF.1.0/boot_images/Build/LahainaLAA/Core/RELEASE_CLANG100LINUX/AARCH64/Sm8350FamilyPkg/Library/MsManufacturingModeDxeLib/MsManufacturingModeDxeLib/MsManufacturingModeDxeLib.makefile
  - MODULE_TYPE                    = DXE_DRIVER
    - This module is a part of DEX_DRIVER but not an indepentant module. It only be used as a library for other DEX_DRIVER.
  - LIBRARY_CLASS                  = MsManufacturingModeLib|DXE_DRIVER DXE_RUNTIME_DRIVER UEFI_APPLICATION
    - https://edk2-docs.gitbook.io/edk-ii-inf-specification/3_edk_ii_inf_file_format/34_-defines-_section#summary
    - https://edk2-docs.gitbook.io/edk-ii-module-writer-s-guide/3_module_development/33_additional_steps_for_library_instances
      - MsManufacturingModeLib: library name referred by other module
      - DXE_DRIVER DXE_RUNTIME_DRIVER UEFI_APPLICATION: these types of modules can use this library
- [Sources]
```
 MsManufacturingModeDxeLib.c
```
## MsManufacturingModeDxeLib.c
- MsGetUefiRuntimeMode
```
/**
  This function is used by all non-MfgMode drivers to determine the current
  Manufacturing Mode. It returns the current mode.

  NOTE: If anything goes wrong internally to this function, or if a
        corrupted/insecure variable is detected, this function will
        default to CUSTOMER_MODE.

  @retval     Current mode or CUSTOMER_MODE if an error occurs.
**/
MS_UEFI_RUNTIME_MODE
EFIAPI
MsGetUefiRuntimeMode (
  VOID
  )
```
- The other functions are not called for c1 project.

# BOOT.MXF.1.0/boot_images/boot/Sm8350FamilyPkg/Library/PlatformKeyBaseLib/
## PlatformKeyBaseLib.inf
- [Defines]
  - This module is a platform base library.
```
  BASE_NAME                      = PlatformKeyBaseLib
  MODULE_TYPE                    = BASE
  LIBRARY_CLASS                  = PlatformKeyLib
```
- [Sources]
```
  PlatformKeyBaseLib.c
```
## PlatformKeyBaseLib.c
- DevelopmentMfgModeVerifyCertificate
```
CONST UINT8  *DevelopmentMfgModeVerifyCertificate = NULL;
CONST UINT32  DevelopmentSizeOfMfgModeVerifyCertificate = 0;
```
- kaDevelopmentPlatformKeyCertificate
  - \#ifndef SHIP_MODE
```
//
// DER encode the cert and then run BinToH.exe
// This certificate is located in:
// Certs/TestCerts/OEMC1_UEFI_PK_SIGNER.cer
//
CONST UINT8 kaDevelopmentPlatformKeyCertificate[] =
{
 0x30, 0x82, 0x03, 0xD5, 0x30, 0x82, 0x02, 0xBD, 0xA0, 0x03, 0x02, 0x01, 0x02, 0x02, 0x10, 0x52,
:
 0xB0, 0x2C, 0x77, 0x3D, 0xDE, 0x0D, 0x29, 0xEB, 0x88,
};

//
// Test/Development Certificate
// This is used as for local MFG mode / Debug Mode unlock
//
CONST UINT8 *DevelopmentPlatformKeyCertificate = kaDevelopmentPlatformKeyCertificate;
CONST UINT32 DevelopmentSizeOfPlatformKeyCertificate = sizeof(kaDevelopmentPlatformKeyCertificate);
```
- kaProductionPlatformKeyCertificate
  - secure boot
```
/** PRODUCTION KEYS  **/

//
// This is the production certficate: 236174_403063_Surface_LFF3_UEFI_PK_Signer_2019.cer
//

CONST UINT8 kaProductionPlatformKeyCertificate[] =
{
  0x2D, 0x2D, 0x2D, 0x2D, 0x2D, 0x42, 0x45, 0x47, 0x49, 0x4E, 0x20, 0x43, 0x45, 0x52, 0x54, 0x49,
  0x46, 0x49, 0x43, 0x41, 0x54, 0x45, 0x2D, 0x2D, 0x2D, 0x2D, 0x2D, 0x0D, 0x0A, 0x4D, 0x49, 0x49,
:
  0x41, 0x54, 0x45, 0x2D, 0x2D, 0x2D, 0x2D, 0x2D, 0x0D, 0x0A,
};

//
// Production Secure Boot PK Certificate
// Populate the Secure Boot PK with this variable.
//
CONST UINT8  *ProductionPlatformKeyCertificate = kaProductionPlatformKeyCertificate;
CONST UINT32  ProductionSizeOfPlatformKeyCertificate = sizeof(kaProductionPlatformKeyCertificate);
```
- kaInternalProductionMfgModeKeyCertificate
```
// Production MfgMode certificate
// Also used for Debug Mode verification
// This should be the CA not the actual leaf signer.
//
// This is the production MfgMode certficate.
// The certificate is statically allocated below, but referenced by the pointer.
// Microsoft Surface FFF 3 Firmware Debug CA 2018.cer
CONST UINT8 kaInternalProductionMfgModeKeyCertificate[] =
{
 0x30, 0x82, 0x07, 0x66, 0x30, 0x82, 0x05, 0x4E, 0xA0, 0x03, 0x02, 0x01, 0x02, 0x02, 0x13, 0x33,
:
 0x43, 0x68, 0x5B, 0xB8, 0x20, 0x19, 0x8A, 0x8F, 0xC4, 0x50,
};
CONST UINT8  *ProductionMfgModeVerifyCertificate = kaInternalProductionMfgModeKeyCertificate;
CONST UINT32  ProductionSizeOfMfgModeVerifyCertificate = sizeof(kaInternalProductionMfgModeKeyCertificate);

```


# BOOT.MXF.1.0/boot_images/boot/Sm8350FamilyPkg/Library/MsPlatformManufacturingModeLibNull
## MsPlatformManufacturingModeLib.inf
## MsPlatformManufacturingModeLib.c  

# BOOT.MXF.1.0/boot_images/boot/Sm8350FamilyPkg/Drivers/MsManufacturingModeDxe
## MsManufacturingMode.inf
- This is a DEX_DRIVER because of ENTRY_POINT definition.
- [Defines]
```
  BASE_NAME                      = ManufacturingModeDxe
  MODULE_TYPE                    = DXE_DRIVER
  ENTRY_POINT                    = ManufacturingModeDriverEntry
```
- [Sources]
```
 MsManufacturingMode.c
```
- [Protocols]
```
  gMsManufacturingModeProtocolGuid    ## PRODUCES
```
- out
  - BOOT.MXF.1.0/boot_images/Build/LahainaLAA/Core/RELEASE_CLANG100LINUX/AARCH64/Sm8350FamilyPkg/Drivers/MsManufacturingModeDxe/MsManufacturingMode/OUTPUT/ManufacturingModeDxe.efi

## MsManufacturingMode.c
- EFI_STATUS EFIAPI ManufacturingModeDriverEntry (  IN EFI_HANDLE        ImageHandle,   IN EFI_SYSTEM_TABLE* SystemTable  )
  - Entry function of ManufacturingModeDxe
  - Installs the Manufacturing mode DXE protocol.
  - call function in MsManufacturingModeUtilitiesDxeLib to implement functions for protocol.
- 


## ManufacturingModeInstructions.txt
  - Instructions for enabling UEFI MANUFACTURING_MODE or CUSTOMER_MODE.
  - Not for user but for driver developer.


# MsManufacturingModeDxe lib
## BOOT.MXF.1.0/boot_images/boot/Sm8350FamilyPkg/Drivers/MsManufacturingModeDxe/MsManufacturingMode.inf
- DEX_DRIVER
```
- [Defines]
  BASE_NAME                      = MsManufacturingModeUtilitiesDxeLib
  MODULE_TYPE                    = DXE_DRIVER
```

# BOOT.MXF.1.0/boot_images/boot/Sm8350FamilyPkg/Sm8350FamilyPkg.dec
---
## [PcdsFixedAtBuild]
- security related code
  - Core.dsc.inc over-rides these values
```
  # MS_CHANGE -->

  ##
  ## This PCD controls the Enhanced Key Usage (EKU) that must be present in the leaf
  ## signer certificate in order to unlock a device.  The default value is 0, which
  ## means "do not require an EKU" in the signature to unlock the device for backwards
  ## compatibility.  Then if the product-specific DSC file over-rides this value,
  ## then the verification code will require that the specified EKU is present in the
  ## leaf signer.  This allows us to cut down on the number of Certificate Authorities
  ## (CA's) required and prevents one product from unlocking another one.  The EKU
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


# Sm8350FamilyPkg/Drivers/MsManufacturingModeDxe/MsManufacturingMode.inf
---
## [Defines]
- DXE_DRIVER
```
  BASE_NAME                      = ManufacturingModeDxe
  MODULE_TYPE                    = DXE_DRIVER
```
## [Sources]
```
 MsManufacturingMode.c
```
##[LibraryClasses]
- use some MS libraries
```
  MsManufacturingModeLib
  MsManufacturingModeUtilitiesDxeLib
  HobLib
  XblHlosHobLib
```
# BOOT.MXF.1.0/boot_images/boot/Sm8350FamilyPkg/Drivers/MsManufacturingModeDxe/ManufacturingModeInstructions.txt
---

# BOOT.MXF.1.0/boot_images/boot/Sm8350FamilyPkg/Drivers/MsManufacturingModeDxe/MsManufacturingMode.c
---


# Sm8350FamilyPkg/Library/MsManufacturingModeDxeLib/MsManufacturingModeDxeLib.inf
---

Sm8350FamilyPkg/Library/MsManufacturingModeUtilitiesDxeLib/MsManufacturingModeUtilitiesDxeLib.inf
---

Sm8350FamilyPkg/Library/MsPlatformManufacturingModeLibNull/MsPlatformManufacturingModeLib.inf
---
