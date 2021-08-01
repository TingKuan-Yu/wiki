[[_TOC_]]

# Overview
  This wiki page intend to list Surface Duo special oem fastboot commands.

# Implementation example
## add oem command in FastbootCmds.c
```
Library/FastbootLib/FastbootCmds.c:
         {"oem get-mfg-blob", CmdOemGetMfgBlob}, // MS_CHANGE

```
## declare functions for oem commands in MsFastbootCmds.h
```
Library/FastbootLib/MsFastbootCmds.h:
  VOID CmdOemGetMfgBlob ();
```
## implement functions for oem commands in MsFastbootCmds.c
```
Library/FastbootLib/MsFastbootCmds.c:
   
   VOID CmdOemGetMfgBlob ()
   {
   }
```

# The oem functions for security

- ## fastboot oem get-mfg-blob
  -   Get signature salt from MS_MANUFACTURINGMODE_PROTOCOL

# The oem functions for MANUFACTURING

- ## fastboot oem get-mfg-mode
  -   Get device mode. It is either MANUFACTURING_MODE or CUSTOMER_MODE.

- ## fastboot oem get-mfg-values
  -   RD debug only. Print out the values of below variables on on UART console.
      - ADB_KERNEL_CMD_PARAMETER_NAME
      - SETUPWIZ_KERNEL_CMD_PARAMETER_NAME
      - SELINUX_PERMISSIVE_KERNEL_CMD_PARAMETER_NAME
      - DISPLAY_FACTORY_KERNEL_CMD_PARAMETER_NAME

- ## fastboot oem clear-mfg-mode
  -  Clear below variables.
      - ADB_KERNEL_CMD_PARAMETER_NAME
      - SETUPWIZ_KERNEL_CMD_PARAMETER_NAME
      - SELINUX_PERMISSIVE_KERNEL_CMD_PARAMETER_NAME
      - MANUFACTURING_MODE_SIGNATURE_VARIABLE_NAME

- ## fastboot oem battery-shipmode
  -  Reboot device with OEM_BATTERY_SHIP_MODE reboot reason. The charge app in xbl will set pmic to battery shipmode according this reboot reason.


      {"oem battery-rnrmode", CmdOemBatteryRnrmode}, // MS_CHANGE
      {"oem enable_act", CmdOemEnableActMode}, // MS_CHANGE
      {"oem disable_act", CmdOemDisableActMode}, // MS_CHANGE
      {"oem set-oem-keys", CmdOemSetKeys}, // MS_CHANGE
      {"oem get-oem-keys", CmdOemGetKeys}, // MS_CHANGE
      {"oem get-sfpd-tamper", CmdOemGetSfpdTamper}, // MS_CHANGE
      {"oem clear-sfpd-tamper", CmdOemClearSfpdTamper}, // MS_CHANGE
      {"oem show-devinfo", CmdShowDevInfo }, // MS_CHANGE
      {"oem touch-fw-version", CmdOemTouchFWVersion}, // MS_CHANGE
      {"oem show-hw-devinfo", CmdShowHWDevInfo }, // MS_CHANGE
      {"oem clear-devinforollback", CmdClearDevInfoRollback }, // MS_CHANGE
      {"oem set-display-factory-kernel-param", CmdOemSetDisplayFactoryKernelParam}, // MS_CHANGE
      {"oem clear-display-factory-kernel-param", CmdOemClearDisplayFactoryKernelParam}, // MS_CHANGE
      {"oem get-display-factory-mode", CmdOemGetDispFactoryMode }, // MS_CHANGE