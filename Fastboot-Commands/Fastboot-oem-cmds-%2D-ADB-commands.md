# overview
- oem set-adb-kernel-param
- oem clear-adb-kernel-param
- code
```
#ifndef SHIP_MODE
      {"oem set-adb-kernel-param", CmdOemSetAdbKernelParam}, // MS_CHANGE
      {"oem clear-adb-kernel-param", CmdOemClearAdbKernelParam}, // MS_CHANGE
:
#endif
```