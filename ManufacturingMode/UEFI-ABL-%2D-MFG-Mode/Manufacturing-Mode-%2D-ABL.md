# Overview
- fastboot oem commands for mfg mode 
- Location of Source code
  - bootable/bootloader/edk2/QcomModulePkg

# fastboot oem commands for mfg mode 

## fastboot oem get-mfg-blob
- run "fastboot oem get-mfg-blob"
```
PS /D/c1/security/mfg_win_unlock> fastboot oem get-mfg-blob
(bootloader) SIGNATURE SALT BEGIN --->

(bootloader) 8E4F37C2166762E3ECB24341E3EFCA8D
(bootloader) 066429515E44CA8398731114EA8E83C1
(bootloader) <--- SIGNATURE SALT END

OKAY [  0.001s]
Finished. Total time: 0.001s
```

## fastboot getvar has-slot:set-mfg-blob
- run "fastboot getvar has-slot:set-mfg-blob"
```
PS /D/c1/security/mfg_win_unlock> fastboot getvar has-slot:set-mfg-blob
getvar:has-slot:set-mfg-blob                       FAILED (remote: 'GetVar Variable Not found')
Finished. Total time: 0.002s
```

## clean manufacturing mode
```
root@TonyYuLinux1:/D/Task/159334-abl-yellow-mode-bad-display# fastboot oem clear-mfg-mode
...
(bootloader) Cleared Manufacturing Mode variable
OKAY [  0.008s]
finished. total time: 0.008s
```


# Related Files
 - Library/avb/
   - VerifiedBoot.c
 - Library/BootLib/
   - DeviceInfo.c
 - Library/BootLib/
   - FastbootMenu.c
 - Library/BootLib/
   - UpdateCmdLine.c
 - Library/BootLib/
   - VerifiedBootMenu.c
 - Library/FastbootLib/
   - FastbootCmds.c
 - Library/FastbootLib/
   - MsFastbootCmds.c
 - Include/Library/
   - MsManufacturingModeLiveLib.h
 - Library/MsManufacturingModeLiveLib/
   - MsManufacturingModeLiveLib.c

# MsManufacturingModeLiveLib
## Include/Library/MsManufacturingModeLiveLib.h


## Library/MsManufacturingModeLiveLib/MsManufacturingModeLiveLib.c

