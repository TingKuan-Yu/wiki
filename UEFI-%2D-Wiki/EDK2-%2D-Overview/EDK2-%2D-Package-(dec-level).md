# Reference
- https://edk2-docs.gitbook.io/edk-ii-uefi-driver-writer-s-guide/30_building_uefi_drivers/302_create_edk_ii_package
- https://edk2-docs.gitbook.io/edk-ii-module-writer-s-guide/1_the_basics_of_edk_ii/11_overview

# What is a Package

- A package is a group of **zero or more modules**. A package must contain a package metadata file (DEC), and possibly a platform metadata file (DSC).

- Functionally, a package is a l**ogical division of a project**. Developers depend on reasonable judgment, such as license or specification compliance, to determine **where** to place a module. These metadata files and the module's INF files are used by the EDK II build system to automatically generate makefiles and a single module tip or whole flash tip, according to the build options used.

# Example of Sm8350FamilyPkg
## BOOT.MXF.1.0/boot_images/boot/Sm8350FamilyPkg/Sm8350FamilyPkg.dec


## BOOT.MXF.1.0/boot_images/boot/QcomPkg/SocPkg/Kodiak/LAA/Core.dsc
- 