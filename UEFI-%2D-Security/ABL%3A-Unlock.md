# Library/BootLib/DeviceInfo.c
- Check unlock with manufacturing mode
```
BOOLEAN IsUnlocked (VOID)
{
  return (DevInfo.is_unlocked ||
          (MsGetUefiRuntimeModeLive() == MANUFACTURING_MODE)); // MS_CHANGE manufacturing mode impiles device unlocked
}

BOOLEAN IsUnlockCritical (VOID)
{
  return (DevInfo.is_unlock_critical ||
          (MsGetUefiRuntimeModeLive() == MANUFACTURING_MODE)); // MS_CHANGE manufacturing mode impiles device unlocked
}
```