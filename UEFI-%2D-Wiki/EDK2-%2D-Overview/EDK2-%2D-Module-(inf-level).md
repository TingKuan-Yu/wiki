# Reference
- https://edk2-docs.gitbook.io/edk-ii-module-writer-s-guide/1_the_basics_of_edk_ii/11_overview

# Module
---
## What is a Module?
- A module is the smallest piece of separately **compile-able code** or **pre-built binary.** 
- It contains a metadata file (INF) plus source code or binary. 
  - The INF file is required by the EDKII build system to describe a module's behavior, such as produced or consumed library classes, ppis, guids, protocols, pcds, and other information.

## Examplf of ColorbarsDxe
- BOOT.MXF.1.0/boot_images/boot/Sm8350FamilyPkg/Drivers/ColorbarsDxe/ColorbarsDxe.inf
  - DEX driver but not UEFI driver
```
[Defines]
  INF_VERSION                    = 0x00010017
  BASE_NAME                      = ColorbarsDxe
  FILE_GUID                      = 7A26D1BD-0557-4B78-8CA1-1E40C7AD9F4D
  MODULE_TYPE                    = DXE_DRIVER
  VERSION_STRING                 = 1.0
  ENTRY_POINT                    = ColorbarsDxeInit

[Sources]
  ColorbarsDxe.c
```
- boot_images/boot/Sm8350FamilyPkg/Drivers/ColorbarsDxe/ColorbarsDxe.c
  - Entry is ColorbarsDexInit
  - use event to call ColorbarsDxeEndOfDxeCallback for setting color bar.
```
/**
Main entry for this driver.

@param ImageHandle     Image handle this driver.
@param SystemTable     Pointer to SystemTable.

@retval EFI_STATUS
**/
EFI_STATUS
EFIAPI
ColorbarsDxeInit(
  IN EFI_HANDLE           ImageHandle,
  IN EFI_SYSTEM_TABLE     *SystemTable)
{
  EFI_STATUS  Status;
  EFI_EVENT   EndOfDxeEvent;

  Status = gBS->CreateEventEx (EVT_NOTIFY_SIGNAL,
                               TPL_CALLBACK,
                               ColorbarsDxeEndOfDxeCallback,
                               NULL,
                               &gEfiEndOfDxeEventGroupGuid,
                               &EndOfDxeEvent);

  return Status;
}

```