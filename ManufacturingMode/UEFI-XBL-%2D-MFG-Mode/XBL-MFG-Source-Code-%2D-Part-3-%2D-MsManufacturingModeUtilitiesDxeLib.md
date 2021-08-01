# Source Location ## BOOT.MXF.1.0/boot_images/boot/Sm8350FamilyPkg/Library/MsManufacturingModeUtilitiesDxeLib/

# MsManufacturingModeUtilitiesDxeLib.inf
## [Defines]
- This is a Library but not a DXE_DRIVER. 
- The LIBRARY_CLASS defines MsManufacturingModeUtilitiesDxeLib without supported types, so this driver is designed for DXE driver.
 - reference for LIBRARY_CLASS - https://edk2-docs.gitbook.io/edk-ii-uefi-driver-writer-s-guide/3_foundation/36_protocols_and_handles/364_multiple_protocol_instances
```
  BASE_NAME                      = MsManufacturingModeUtilitiesDxeLib
  MODULE_TYPE                    = DXE_DRIVER
  LIBRARY_CLASS                  = MsManufacturingModeUtilitiesDxeLib
```
## [Sources]
```
 MsManufacturingModeUtilitiesDxeLib.c
```

## [Packages]
- This driver uses **CryptoPkg** and **SecurityPkg**. These two packages are EDK2 original packages.
```
  CryptoPkg/CryptoPkg.dec
  SecurityPkg/SecurityPkg.dec
  Sm8350FamilyPkg/Sm8350FamilyPkg.dec
  QcomPkg/QcomPkg.dec
```

## [LibraryClasses]
- This driver use **security keys** in PlatformKeyLib and functions in other libraries.
```
  PlatformKeyLib
  MsPlatformManufacturingModeLib
  BaseCryptLib
```

# MsManufacturingModeUtilitiesDxeLib.c  
## EFI_STATUS EFIAPI IsManufacturingModeEnabled( OUT UINT8* IsEnabled )
- This is the key function for detecting MFG mode
- flow
  -  1)  Looks to see if the manufacturing mode **signature** is present.
  -  2)  If the **signature** is present, read the **challenge**.
         The data that was signed is the 32 bytes of challenge that we generated.
  -  3)  Verify that the signature is valid for this unit.
  -  4)  Verify that the leaf signer certificate was issued by a Certificate Authority (CA) that we trust.


# ManufacturingModeInstructions.txt  
