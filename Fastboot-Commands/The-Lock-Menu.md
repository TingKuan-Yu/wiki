# Reproduce unlock menu
## 1. Device is NOT at mfg mode
- If device is at mfg mode, the lock menu will not be shown on display.

## 2. use flash_customer.sh to flash customer_combo
```
------------------------------------------
E-OS DEVICE FLASH
combo build version: unknown unknown
------------------------------------------

   * Skipping ADB

Linux

> Check for a Fastboot Device
   * Fastboot device found
Is secure device? False
0
> fastboot  oem clear-display-factory-kernel-param
(bootloader) 
Display Factory Kernel Param Cleared.

OKAY [  0.007s]
Finished. Total time: 0.007s
> fastboot  flashing lock
OKAY [  0.024s]
Finished. Total time: 0.024s
> fastboot  erase misc
Erasing 'misc'                                     OKAY [  0.067s]
Finished. Total time: 0.073s
> fastboot  oem clear-mfg-mode
```
## 3. The device screen shows below message
```
<!>
If you lock the bootloader, you will not be able to install custom
operating system software on this phone.

To prevent unauthorized access to your personal data, locking 
the bootloader will also delete all personal data on your phone.

Press Volume Up or Down button to change selection
Press Power button to select

-------------------------------
DO NOT LOCK THE BOOTLOADER

-------------------------------
LOCK THE BOOTLOADER

-------------------------------
```

# issue recovery failed
---
## fix file
[UnlockMenu.c-fix.txt](/.attachments/UnlockMenu.c-fix-929ac706-0ab7-418a-9da5-9f4fc4eafd37.txt)

## patch
```
1. mUnlockInfo
STATIC UNLOCK_INFO mUnlockInfo[] = {
        [DISPLAY_MENU_LOCK] = {UNLOCK, TRUE},
        [DISPLAY_MENU_UNLOCK] = {UNLOCK, FALSE},
        [DISPLAY_MENU_LOCK_CRITICAL] = {UNLOCK_CRITICAL, TRUE},
        [DISPLAY_MENU_UNLOCK_CRITICAL] = {UNLOCK_CRITICAL, FALSE},
};

2. STATIC MENU_MSG_INFO mLockMenuMsgInfo[] = {
    {{"DO NOT LOCK THE BOOTLOADER"},
     COMMON_FACTOR,
     BGR_WHITE,
     BGR_BLACK,
     OPTION_ITEM,
     0,
     RECOVER}, --> from RESTART

    {{"LOCK THE BOOTLOADER"},
     COMMON_FACTOR,
     BGR_WHITE,
     BGR_BLACK,
     OPTION_ITEM,
     0,
     RESTART},--> from RECOVER

3. ResetDeviceUnlockStatus (INTN Type) --> ADD DEBUG LOG
  DEBUG ((EFI_D_INFO, "ResetDeviceUnlockStatus: Type: %d\n", Type));
  DEBUG ((EFI_D_INFO, "ResetDeviceUnlockStatus: mUnlockInfo[Type].UnlockType %d\n", mUnlockInfo[Type].UnlockType));
  DEBUG ((EFI_D_INFO, "ResetDeviceUnlockStatus: mUnlockInfo[Type].UnlockValue %d\n", mUnlockInfo[Type].UnlockValue));

```

# Call flow
---
## bootable/bootloader/edk2/QcomModulePkg/Library/FastbootLib/FastbootCmds.c
- SetDeviceUnlock (UINT32 Type, BOOLEAN State)
  - Only be call when **MsGetUefiRuntimeModeLive () == CUSTOMER_MODE**
  - The user may unlock the device manually, so alarm user that the device is going to be locked.
```
SetDeviceUnlock (UINT32 Type, BOOLEAN State)
{

  if ((MsGetUefiRuntimeModeLive () == CUSTOMER_MODE) && // MS_CHANGE Disable prompt for MANUFACTURING_MODE
      (GetAVBVersion () != AVB_LE) &&
      is_display_supported () &&
      IsEnableDisplayMenuFlagSupported ()) {
    Status = DisplayUnlockMenu (Type, State);
    if (Status != EFI_SUCCESS) {
      FastbootFail ("Command not support: the display is not enabled");
      return;
    } else {
      FastbootOkay ("");
    }
  }

}
```
- CmdFlashingUnlock(), CmdFlashingLock(), CmdFlashingLockCritical() and CmdFlashingUnLockCritical() call SetDeviceUnlock()
```
#ifdef ENABLE_UPDATE_PARTITIONS_CMDS
STATIC VOID
CmdFlashingUnlock (CONST CHAR8 *arg, VOID *data, UINT32 sz)
{
  SetDeviceUnlock (UNLOCK, TRUE);
}

STATIC VOID
CmdFlashingLock (CONST CHAR8 *arg, VOID *data, UINT32 sz)
{
  SetDeviceUnlock (UNLOCK, FALSE);
}
#endif

#ifdef ENABLE_DEVICE_CRITICAL_LOCK_UNLOCK_CMDS
STATIC VOID
CmdFlashingLockCritical (CONST CHAR8 *arg, VOID *data, UINT32 sz)
{
  SetDeviceUnlock (UNLOCK_CRITICAL, FALSE);
}

STATIC VOID
CmdFlashingUnLockCritical (CONST CHAR8 *arg, VOID *data, UINT32 sz)
{
  SetDeviceUnlock (UNLOCK_CRITICAL, TRUE);
}
#endif
```
- oem unlock functions
```
#ifdef ENABLE_UPDATE_PARTITIONS_CMDS
      {"flashing unlock", CmdFlashingUnlock},
      {"flashing lock", CmdFlashingLock},
#endif
#ifdef ENABLE_DEVICE_CRITICAL_LOCK_UNLOCK_CMDS
      {"flashing unlock_critical", CmdFlashingUnLockCritical},
      {"flashing lock_critical", CmdFlashingLockCritical},
#endif
```

# bootable/bootloader/edk2/QcomModulePkg/Library/BootLib/UnlockMenu.c
---
## STATIC EFI_STATUS UnlockMenuShowScreen (OPTION_MENU_INFO *OptionMenuInfo, INTN Type, BOOLEAN Value)
- lock - mLockMenuMsgInfo, unlock - mUnlockMenuMsgInfo
```
STATIC EFI_STATUS
UnlockMenuShowScreen (OPTION_MENU_INFO *OptionMenuInfo,
                      INTN Type,
                      BOOLEAN Value)
{
:


  if (Value) {
    OptionMenuInfo->Info.MsgInfo = mUnlockMenuMsgInfo;
    MaxLine = ARRAY_SIZE (mUnlockMenuMsgInfo);
  } else {
    OptionMenuInfo->Info.MsgInfo = mLockMenuMsgInfo;
    MaxLine = ARRAY_SIZE (mLockMenuMsgInfo);
  }

:
}
```


## EFI_STATUS DisplayUnlockMenu (INTN Type, BOOLEAN Value)
```
/**
  Draw the unlock menu and start to detect the key's status
  @param[in] Type       The type of the unlock menu
                        [UNLOCK]: The normal unlock menu
                        [UNLOCK_CRITICAL]: The ctitical unlock menu
             Value      [TRUE]: Unlock menu
                        [FALSE]: Lock menu
  @retval EFI_SUCCESS   The entry point is executed successfully.
  @retval other         Some error occurs when executing this entry point.
**/
EFI_STATUS
DisplayUnlockMenu (INTN Type, BOOLEAN Value)
{
  EFI_STATUS Status = EFI_SUCCESS;
  OPTION_MENU_INFO *OptionMenuInfo;

  if (IsEnableDisplayMenuFlagSupported ()) {
    OptionMenuInfo = &gMenuInfo;
    DrawMenuInit ();

    /* Initialize the last menu type */
    OptionMenuInfo->LastMenuType = OptionMenuInfo->Info.MenuType;

    Status = UnlockMenuShowScreen (OptionMenuInfo, Type, Value);
    if (Status != EFI_SUCCESS) {
      DEBUG ((EFI_D_ERROR, "Unable to show %a menu on screen: %r\n",
              Value ? "Unlock" : "Lock", Status));
      return Status;
    }

    MenuKeysDetectionInit (OptionMenuInfo);
    DEBUG ((EFI_D_VERBOSE, "Creating unlock keys detect event\n"));
  } else {
    DEBUG ((EFI_D_INFO, "Display menu is not enabled!\n"));
    Status = EFI_NOT_STARTED;
  }

  return Status;
}
```

## mLockMenuMsgInfo
```
STATIC MENU_MSG_INFO mLockMenuMsgInfo[] = {
    //MSCHANGE DRAW Later
    //{{"<!>"}, BIG_FACTOR, BGR_RED, BGR_BLACK, COMMON, 0, NOACTION},
    {{"\n\nIf you lock the bootloader, you will not be able to install "
      "custom operating system software on this phone.\n"},
     COMMON_FACTOR,
     BGR_WHITE,
     BGR_BLACK,
     COMMON,
     0,
     NOACTION},
    {{"\nTo prevent unauthorized access to your personal data, "
      "locking the bootloader will also delete all personal "
      "data on your phone.\n"},
     COMMON_FACTOR,
     BGR_WHITE,
     BGR_BLACK,
     COMMON,
     0,
     NOACTION},
    {{"\nPress Volume Up or Down button to change selection\n"
      "Press Power button to select\n"},
     COMMON_FACTOR,
     BGR_WHITE,
     BGR_BLACK,
     COMMON,
     0,
     NOACTION},
    {{"__________"},
     COMMON_FACTOR,
     BGR_WHITE,
     BGR_BLACK,
     LINEATION,
     0,
     NOACTION},
    {{"DO NOT LOCK THE BOOTLOADER"},
     COMMON_FACTOR,
     BGR_WHITE,
     BGR_BLACK,
     OPTION_ITEM,
     0,
     RESTART},
    {{"__________"},
     COMMON_FACTOR,
     BGR_WHITE,
     BGR_BLACK,
     LINEATION,
     0,
     NOACTION},
    {{"LOCK THE BOOTLOADER"},
     COMMON_FACTOR,
     BGR_WHITE,
     BGR_BLACK,
     OPTION_ITEM,
     0,
     RECOVER},
    {{"__________"},
     COMMON_FACTOR,
     BGR_WHITE,
     BGR_BLACK,
     LINEATION,
     0,
     NOACTION},
};

```
