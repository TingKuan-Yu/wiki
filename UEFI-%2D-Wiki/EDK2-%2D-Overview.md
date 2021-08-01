# Reference
- https://edk2-docs.gitbook.io/edk-ii-module-writer-s-guide/1_the_basics_of_edk_ii/11_overview

# What is a Module?
- A module is the smallest piece of separately compile-able code or pre-built binary. It contains a metadata file (INF) plus source code or binary. 
- The INF file is required by the EDKII build system to describe a module's behavior, such as produced or consumed library classes, ppis, guids, protocols, pcds, and other information.
- For example, in $WORKSPACE\MdeModulePkg\Universal\Bus\Pci\UhciDxe, the source files mentioned and the INF file compose a module.
- Refer to the EDK II Extended INF Specification. for the syntax of the INF file.
  - https://edk2-docs.gitbook.io/edk-ii-inf-specification/

# What is a Package?
- A package is a group of zero or more modules. A package must contain a package metadata file (DEC), and possibly a platform metadata file (DSC).
- Functionally, a package is a logical division of a project. Developers depend on reasonable judgment, such as license or specification compliance, to determine where to place a module. These metadata files and the module's INF files are used by the EDK II build system to automatically generate makefiles and a single module tip or whole flash tip, according to the build options used.
- For information regarding the syntax of DSC and DEC files, please refer to EDK II DSC File Specification and EDK II DEC File Specification.
  - https://edk2-docs.gitbook.io/edk-ii-dec-specification/

# What is a Platform?
- A platform is a **special type of package** with additional metadata files. 
- A platform  (special type of package) must contain one DSC file and zero or one FDF file. The FDF is only required if flash output is required.
- Refer to EDK II FDF File Specification for information regarding FDF files.
  - https://edk2-docs.gitbook.io/edk-ii-fdf-specification/
  - https://edk2-docs.gitbook.io/edk-ii-dsc-specification/