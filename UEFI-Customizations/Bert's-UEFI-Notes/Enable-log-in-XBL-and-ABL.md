[[_TOC_]]



# BOOT related code
- **QcomPkg/Include/Library/DebugLib.h:**
```
//
// Declare bits for PcdDebugPrintErrorLevel and the ErrorLevel parameter of DebugPrint()
//
#define DEBUG_INIT      0x00000001  // Initialization
#define DEBUG_WARN      0x00000002  // Warnings
#define DEBUG_LOAD      0x00000004  // Load events
#define DEBUG_FS        0x00000008  // EFI File system
#define DEBUG_POOL      0x00000010  // Alloc & Free's
#define DEBUG_PAGE      0x00000020  // Alloc & Free's
#define DEBUG_INFO      0x00000040  // Informational debug messages
#define DEBUG_DISPATCH  0x00000080  // PEI/DXE/SMM Dispatchers
#define DEBUG_VARIABLE  0x00000100  // Variable
#define DEBUG_BM        0x00000400  // Boot Manager
#define DEBUG_BLKIO     0x00001000  // BlkIo Driver
#define DEBUG_NET       0x00004000  // SNI Driver
#define DEBUG_UNDI      0x00010000  // UNDI Driver
#define DEBUG_LOADFILE  0x00020000  // UNDI Driver
#define DEBUG_EVENT     0x00080000  // Event messages
#define DEBUG_GCD       0x00100000  // Global Coherency Database changes
#define DEBUG_CACHE     0x00200000  // Memory range cachability changes
#define DEBUG_VERBOSE   0x00400000  // Detailed debug messages that may significantly impact boot performance
#define DEBUG_ERROR     0x80000000  // Error
```

- **QcomPkg/SocPkg/Kodiak/WP/Core.dsc**
```
!if $(PRODMODE) == "PRODMODE"
  # Only enable Errors and Boot Manager if Production Mode Flag is set
  gEfiMdePkgTokenSpaceGuid.PcdDebugPrintErrorLevel|0x80000400
  gEfiMdePkgTokenSpaceGuid.PcdFixedDebugPrintErrorLevel|0x80000400
!else
  gEfiMdePkgTokenSpaceGuid.PcdDebugPrintErrorLevel|0x800fee0f
  gEfiMdePkgTokenSpaceGuid.PcdFixedDebugPrintErrorLevel|0x800fee0f
!endif
```

# edk2 related code
- edk2/QcomModulePkg/QcomModulePkg.dsc
```
  gEfiMdePkgTokenSpaceGuid.PcdDebugPrintErrorLevel|0x80000042
```



# Qualcomm Document
- **Enable verbose log in ABL(UEFI)**
KBA number: KBA-181015040330
Applicable platform: Generic
- **Description:**
By default the log in UEFI is only enable ERROR level for performance. When debug we need to enable VERBOSE level.
- **Solutions:**
 add below change in bootable/bootloader/edk2/QcomModulePkg/QcomModulePkg.dsc
```
- gEfiMdePkgTokenSpaceGuid.PcdDebugPrintErrorLevel|0x80000042
+ gEfiMdePkgTokenSpaceGuid.PcdDebugPrintErrorLevel|0x80400042
```

# Reference
- https://github.com/tianocore/tianocore.github.io/wiki/EDK-II-Debugging