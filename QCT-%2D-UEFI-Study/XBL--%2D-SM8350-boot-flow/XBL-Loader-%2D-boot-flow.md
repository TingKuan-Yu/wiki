# BOOT.MXF.1.0/boot_images/boot/QcomPkg/SocPkg/Library/XBLLoaderLib/XBLLoaderLib.inf
## [Defines]
- Non UEFI library
- out:
BOOT.MXF.1.0/boot_images/Build/LahainaLAA/Loader/RELEASE_CLANG100LINUX/AARCH64/QcomPkg/SocPkg/Library/XBLLoaderLib/XBLLoaderLib/OUTPUT/**XBLLoaderLib.lib**
- source
```
  BASE_NAME                      = XBLLoaderLib 
  MODULE_TYPE                    = BASE
  LIBRARY_CLASS                  = XBLLoaderLib
```
## [Sources.AARCH64]
- source - **sbl1_Aarch64.s**
```
  sbl1_Aarch64.s |GCC
  sbl1_sdi_Aarch64.s |GCC
  sbl1_mc.c
  sbl1_target.c
  sbl1_config.c
```

# BOOT.MXF.1.0/boot_images/boot/QcomPkg/SocPkg/Library/XBLLoaderLib/sbl1_Aarch64.s
## _main:
- BL sbl1_main_ctl
```
sbl1_entry:
:
sbl1_entry_init_stack:  
  // -------------------------------
  // add more assembly init code here for entering sbl1_main_ctl	
  // 
  // restore PBL parameter and enter sbl1_main_ctl
  // -------------------------------
  MOV w0, w7
  BL sbl1_main_ctl

```

# BOOT.MXF.1.0/boot_images/boot/QcomPkg/SocPkg/Library/XBLLoaderLib/sbl1_mc.c
## void sbl1_main_ctl(boot_pbl_shared_data_type *pbl_shared)
- @brief
   The  Main Controller performs the following functions:
      - Initializes ram
      - And so on...
- @par Side Effects
   This function never return

- source
  - After initialization, invoke "status = sbl1_config_process_bl(config_context_handle, sbl1_config_table)".
```
void sbl1_main_ctl(boot_pbl_shared_data_type *pbl_shared)
{
:


  do
  {
    /* Calculate the SBL start time for use during boot logger initialization. */
: 
    /* Initialize dal heap using internal memory */
: 
    /* Initialize DAL, needs to be called before modules that uses DAL */
:  
   /* Enable qdss workaround */
:  
   /* Initialize the stack protection canary */
:
   /* Retrieve info passed from PBL*/
:
    /* Initialize SBL memory map */
:
    /* Initialize busywait module Note: required before logger init due to uart driver dependency on busywait */
:
    /* Initialize boot shared imem */
:
    /* Initialize the ChipInfo driver */
:
    /* Initialize boot statistics */
:
    /* Initialize boot logger and start the log timer.
    This must be done after sbl1_retrieve_shared_info_from_pbl
    and boot_secboot_ftbl_init. */
:
    /* Initialize the QSEE interface */
    sbl1_init_sbl_qsee_interface(config_context_handle, &sbl_verified_info);

    //TODO: FIXME
    /* Set hash algorithm */
    //  BL_VERIFY(boot_set_hash_algo(SBL_HASH_SHA256) == BL_ERR_NONE, BL_ERR_UNSUPPORTED_HASH_ALGO|BL_ERROR_GROUP_BOOT);

    /* Call sbl1_hw_init to config pmic device so we can use PS_HOLD to reset */
    status = sbl1_hw_init(config_context_handle);
    if(status != BL_ERR_NONE)
    {
      break;
    }

#ifdef FEATURE_DEVICEPROGRAMMER_IMAGE
    /* Check if we need to branch to device programmer */
    device_programmer_lite_check(config_context_handle);
    device_programmer_ddr_check(config_context_handle);
#endif


    //TODO: FIXME
    /* Store the sbl1 hash to shared imem */
    // boot_store_tpm_hash_block(&bl_shared_data, &sbl_verified_info);

    /*-----------------------------------------------------------------------
    Process the target-dependent SBL1 procedures
    -----------------------------------------------------------------------*/
    status = sbl1_config_process_bl(config_context_handle, sbl1_config_table);
    if(status != BL_ERR_NONE)
    {
      break;
    }

  }
  while (FALSE);
  
  error_if.error_handler(__FILE_BASENAME__, __LINE__, status);
  
} /* sbl1_main_ctl() */

```

