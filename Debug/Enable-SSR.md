https://dev.azure.com/E-OS/Zeta/_workitems/edit/146700/

Fastboot oem command (these commands will be gone in SHIP_MODE):
```
set-customized-kernel-param
extend-customized-kernel-param
clear-customized-kernel-param
```

Linux Kernel Param:
```
androidboot.ssr.restart.level=<Restart Level>
For example: androidboot.ssr.restart.level=ALL_ENABLE

Adb Check:
getprop ro.boot.ssr.restart.level
getprop persist.vendor.ssr.restart_level


```
