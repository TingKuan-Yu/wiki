
# Introduction
   This page shows debug message from UART log about details of MS boot mode Color Bar. 

# Reference
- QC document 80-PK177-40
  - for security status

# Uart log
## YELLOW - not FULLY FUSED
```
[ColorbarsDxeEndOfDxeCallback] ProductionDeviceCheckResult: 0
[ColorbarsDxeEndOfDxeCallback] RpmbCheckResult: 0
[ColorbarsDxeEndOfDxeCallback] RollbackCheckResult: 0
[ColorbarsDxeEndOfDxeCallback] Device is not fully fused, drawing yellow colorbar```
```

## ORANGE - NOT Fused
```
[ColorbarsDxeEndOfDxeCallback] Device is not fused at all, drawing orange colorbar
```
## GREEN - NOT Ship Mode Build
```
[ColorbarsDxeEndOfDxeCallback] SHIP_MODE is off, drawing green colorbar
```
## PURPLE - At MFG Mode
```
[ColorbarsDxeEndOfDxeCallback] - Device in Manufacturing Mode, drawing purple colorbar
```

# Source Code for uart logs
## boot/QcomPkg/Library/FuseControlLib/FuseControlLib.c
- IsProductionDevice(void)
  - bit 0
    - Secure Boot enabled/disabled
  - bit 1
    - SHK probgrammed yes/no
  - bit 2
    - All Debug Disabled (Roll-up of TZ, Modem, Content Protection and Non-secure debug)
  - bit 6
    - Debug Enabled (DEBUG_OU flag setting in xbl image or Debug Policy JTAG flag)

```
/**
 Check if this is a production device

  @retval TRUE if it is
  @retval FALSE if it is not

**/
BOOLEAN 
EFIAPI
IsProductionDevice(void)
{
    UINT32 secure_state = 0;
    
    secure_state = GetSecurityState();
    if( ERROR_SECURITY_STATE == secure_state ) {
        return FALSE;
    }
    // Bit#0 = 0 AND Bit#1 = 0 AND Bit#2 = 0 AND Bit#6 = 1 for production Device
    if( (!(secure_state & 0x1) && !((secure_state >> 1) & 0x1) && 
        !((secure_state >> 2) & 0x1) && ((secure_state >> 6) & 0x1) )) {
        return TRUE; // production Device Check PASS
    }
    return FALSE; // Production Device Check FAIL, not a production device
}
```

- IsRpmbProvisioned(void)
  - Bit 5 
   - rpmb provision check
/**
  Check if RPMB is provisioned

  @retval TRUE if it is
  @retval FALSE if it is not

**/
BOOLEAN 
EFIAPI
IsRpmbProvisioned(void)
{
    UINT32 secure_state = 0;
    
    secure_state = GetSecurityState();
    if( ERROR_SECURITY_STATE == secure_state ) {
        return FALSE;
    }
    
    // Bit#5 rpmb provision check
    if(! (((secure_state >> 5) & 0x1)))
        return TRUE; // rpmb provisioned
    
    return FALSE; // rpmb provision Check FAIL
}

- IsRollbackEnabled(void)
  - Bit 3
    - rollback enable check
```
/**
  Check if rollback is enabled

  @retval TRUE if it is
  @retval FALSE if it is not

**/
BOOLEAN 
EFIAPI
IsRollbackEnabled(void)
{
    UINT32 secure_state = 0;

    secure_state = GetSecurityState();
    if( ERROR_SECURITY_STATE == secure_state ) {
        return FALSE;
    }

    // Bit#3 rollback enable check
    if(! (((secure_state >> 3) & 0x1)))
        return TRUE; // rollback enabled

    return FALSE; // rollback check FAIL
}
```
- GetDebugPolicyFlag (&debugPolicyContent);
  - **DrawYellowBar**
```
/*
  * Add DebugPolicyMask for ignoring bit of crashdump in debug policy
  * The mask is the complement of the debug policy for apdp in
  * Lahaina.LA.1.0/common/sectools/config/lahaina/lahaina_debugpolicy.xml
  */
  UINT64 debugPolicyContent = 0;
  DebugPolicyCheckResult = GetDebugPolicyFlag (&debugPolicyContent);      // true  means not fused
  UINT64 debugPolicyMask = PcdGet64(DebugPolicyMask);
  if (DebugPolicyCheckResult == TRUE && (debugPolicyContent & debugPolicyMask) != 0) {
    DEBUG((DEBUG_ERROR, "[%a] DebugPolicyCheckResult: %d, DebugPolicyContent: %lu\n", __FUNCTION__, DebugPolicyCheckResult, debugPolicyContent));
    DrawYellowBar = TRUE;
  }
```