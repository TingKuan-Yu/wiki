
# XBL Loader boot error handler
## BOOT.MXF.1.0/boot_images/boot/QcomPkg/SocPkg/Library/XBLLoaderLib/boot_error_handler.c
- boot_error_handler()
  - @brief
      This function is the error handler for the BOOT and **records the line 
      number, filename & error type before jumping into the downloader**. 
      This function is also **shared by exception handler** and can log
      multiple errors if called more than once.
- Note: if recoverable error, boot to ramdump mode for minidump is ok. If unrecoverable error, no useful methods to avoid being a block device.


## BOOT.MXF.1.0/boot_images/boot/QcomPkg/XBLLoader/ExtDrivers/boot_ramdump.c
- void boot_dload_transition_pbl_forced_dload(void* config_context)
  - @brief
     This function sets the magic numbers for PBL to detect and enter forced download mode.  It then calls the target specific function to trigger a system reset.

## BOOT.MXF.1.0/boot_images/boot/QcomPkg/SocPkg/Library/XBLLoaderLib/sbl1_target.c
- void (*sbl_dload_entry)(void*) = boot_dload_transition_pbl_forced_dload; 
  - @brief
     This function pointer is defined in each SBL Bootloader to handle SBL-specific requirements to enter a download routine. It is initialized to boot_dload_transition_pbl_forced_dload by default.

- bl_error_boot_type sbl1_dload_entry (boot_handle config_context_handle)
  - @brief
   This function is defined in each SBL Bootloader to handle SBL-specific requirements to enter a download routine.
  - **Set in sbl1_mc.c after sbl1_post_ddr_init**

## BOOT.MXF.1.0/boot_images/boot/QcomPkg/SocPkg/Library/XBLLoaderLib/sbl1_mc.c
- void sbl_error_handler(void)
  - @brief
     This fills the boot_crash_dump_data struct for use by simulator tool, and copies it and other boot memory regions to an unused region for dumping

- bl_error_boot_type sbl1_post_ddr_init(boot_handle config_context_handle)
  -  @brief
    This funcion will initialize the data section in DDR and relocate boot log to DDR. After execution of this function SBL1 will enter Sahara in stead of PBL emergency dload mode in case of error.

# Firehose
## BOOT.MXF.1.0/boot_images/boot/QcomPkg/Library/DevPrgLib/devprg_firehose.c
- static int handle_power(struct dp_xml_handle *xml_handle)
```
  switch(power_state)
  {
  case DEVPRG_REBOOT_EDL:
    devprg_target_reset_edl();
    break;
```
## BOOT.MXF.1.0/boot_images/boot/QcomPkg/Library/DevPrgLib/devprg_target.c
- void devprg_target_reset_edl(void)
```
void devprg_target_reset_edl(void)
{
  boot_dload_transition_pbl_forced_dload(CONFIG_CONTEXT_CRT_HANDLE);
}
```

# XBLLoader
## BOOT.MXF.1.0/boot_images/boot/QcomPkg/XBLLoader/ExtDrivers/boot_ramdump.c
- void boot_dload_transition_pbl_forced_dload(void* config_context)
  - register_value |= FORCE_DLOAD_BOOT_USB; --> **for Ship mode, maybe we can remove this**
```
* @brief
*   This function sets the magic numbers for PBL to detect and enter forced
*   download mode.  It then calls the target specific function to trigger a
*   system reset.
void boot_dload_transition_pbl_forced_dload(void* config_context)
{
:
    register_value =HWIO_TCSR_TCSR_BOOT_MISC_DETECT_INM(HWIO_TCSR_TCSR_BOOT_MISC_DETECT_RMSK);
	
	/* Clear any SBL DLOAD, MINIDUMP area */
	register_value &= ~(SBL_DLOAD_MODE_BIT_MASK | SBL_MINIDUMP_MODE_BIT_MASK);
	
    /* Clear the PBL masked area and then apply HS_USB value */
    register_value &= ~(FORCE_DLOAD_MASK);
    register_value |= FORCE_DLOAD_BOOT_USB;

#ifdef QCLIB_IMAGE
     /* Write the new value back out to the register */
    HWIO_TCSR_TCSR_BOOT_MISC_DETECT_OUTM(FORCE_DLOAD_MASK, register_value);
#else
     /* Write the new value back out to the register */
    HWIO_TCSR_TCSR_BOOT_MISC_DETECT_OUT(register_value);
#endif
    reset_if->hw_reset(BOOT_WARM_RESET_TYPE);
  }
  while(FALSE);
} /* boot_dload_transition_pbl_forced_dload() */

```

# TO Study
```
BOOT_RAMDUMP_ENABLE
```
