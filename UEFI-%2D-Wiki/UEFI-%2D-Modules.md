# UEFI SEC Modules
---
## https://edk2-docs.gitbook.io/edk-ii-module-writer-s-guide/6_sec_module
```
The SEC module is the first module executed after power-on. It is responsible for configuring the PEI environment's memory call stack. In addition, this module discovers and passes control to PEI Core and hands information to the PEI Foundation.
- Write the INF File
  - For a physical platform, MODULE_TYPE must be set to SEC. For an Emulation Platform, the SEC module's MODULE_TYPE must be set to SEC or **USER_DEFINED**.
  - For IA-32 Intel Architecture **_ModuleEntryPoint** is the default entry point for the SEC module.
```