# Document
---
## QC doc - SM8350 Boot and CoreBSP Architecture Overview
- Flow 4a-4c. 
  - XBL_Loader initializes hardware and firmware images, CPU caches, MMU, boot devices, XBLConfig, PMIC, DDR, SHRM, and SMEM (shared memory). 
  - XBL_Loader fills platform ID and RAM partition table, performs DDR training if applicable, and executes an SCM call to **XBL_SEC** to initialize Pseudo IMEM (pIMEM). 
  - XBL_Loader also initializes and configures the clock frequencies as per the clock plan; loads and authenticates the APPS debug policy (APDP) image from the boot device. 
  - XBL_Loader loads and authenticates eXtensible boot loader (XBL) RAM dump, if the **DLOAD cookie** is set, and jumps to XBL RAM dump to collect the crash dump. 

# Log
---
## The putty log to ramdump mode
- Warm Reset
```
B -    530029 - PM: Reset by PSHOLD
B -    533262 - PM: Reset Type: Warm Reset
B -    536586 - PM: Warm reset count:0x3
B -    540521 - PM: Reset by PSHOLD
B -    544272 - PM: Reset Type: Warm Reset
B -    547566 - PM: Warm reset count:0x2
B -    551501 - PM: Reset by PSHOLD
B -    555252 - PM: Reset Type: Warm Reset
B -    558577 - PM: Warm reset count:0x1
```
- reset value
```
B -    816820 - PM: Get PMIC Reset Reason Value: 0x46
```
- Load RamDump image
  - with **TCSR reg** log
  - with RamDump log
```
D -     17598 - sbl1_post_ddr_init
D -         0 - sbl1_hw_init_secondary
B -   1035444 - DDR -  Image Load, Start
:
D -       458 - boot_dload_dump_security_regions
B -   1076497 - TCSR reg value 0x10 
D -      4453 - ramdump_load_cancel
B -   1084336 - RamDump -  Image Load, Start
D -       824 - Auth Metadata
D -      2196 - Segments hash check
D -     10675 - RamDump -  Image Loaded, Delta - (362000 Bytes)
B -   1104008 - boot_dload_entry
```
## Putty of Normal boot
- Comparison with ram dump mode
  - no TCSR log
  - The same with RamDump log
```
D -         0 - boot_dload_dump_security_regions
D -         0 - ramdump_load_cancel
B -    985973 - RamDump -  Image Load, Start
D -      3294 - RamDump -  Image Loaded, Delta - (0 Bytes)
D -        30 - boot_update_abnormal_reset_status
```

# Source Code
---

## BOOT.MXF.1.0/boot_images/boot/QcomPkg/SocPkg/Library/XBLLoaderLib/sbl1_config.c
### boot_dload_dump_security_regions
- related log
```
D -       458 - boot_dload_dump_security_regions
```
- BOOT.MXF.1.0/boot_images/boot/QcomPkg/XBLLoader/DloadDump/dload_dump.c
```
/*===========================================================================
**  Function :  boot_dload_dump_security_regions
** ==========================================================================
*/
/*!
* 
* @brief
*   This function will dump backup qsee and qhee regions according to 
*   information passed by qsee/qhee's shared imem cookies, so they can be 
*   ramdumped later.
*
* @param[in] shared_data Pointer to shared data
*        
* @par Dependencies
*   Called only in dload path
* 
*/
```
### ramdump_load_cancel
- related log
```
D -      4453 - ramdump_load_cancel
```
- static bl_error_boot_type ramdump_load_cancel(boot_handle config_context_handle)
  - call boot_dload_entry()
```
/* Conditionally cancel RD loading in SBL1 */
static bl_error_boot_type ramdump_load_cancel(boot_handle config_context_handle)
{
  bl_error_boot_type status = BL_ERR_NONE;

  if(!boot_dload_entry())
  {
    status = boot_config_context_set_value(config_context_handle, CONFIG_CONTEXT_LOAD_FLAG, FALSE);
  }

  return status;
}
```

### boot_configuration_table_entry sbl1_config_table[] 
```
{PBL_MEDIA, SECBOOT_SBL_SW_TYPE,        CONFIG_IMG_ELF,  BOOT_ELF_LOADER_SYNC_LOAD_SYNC_HASH,  TRUE,           TRUE,   TRUE,  FALSE, TRUE,  NULL, sbl1_dload_entry,  xblramdump_pre_procs, NULL,               NULL,             xblramdump_load_metadata, sbl1_partition_id,              SCL_RAMDUMP_CODE_BASE,  0x0,                  ramdump_img_whitelist,  WHITELIST_VALID_ENTRIES(ramdump_img_whitelist),   RAMDUMP_STR     },
```

## BOOT.MXF.1.0/boot_images/boot/QcomPkg/XBLLoader/ExtDrivers/boot_ramdump.c
- boot_dload_entry()
  - snprintf(dbg_info, 40, "TCSR reg value 0x%x ", dload_flag);
  - RETURN VALUE -->  TRUE indicates downloader should be entered.
  - QCLIB_IMAGE is NOT defined in lahaina platform --> use HWIO_TCSR_TCSR_BOOT_MISC_DETECT_OUTM only
```
/*===========================================================================

FUNCTION  BOOT_DLOAD_ENTRY

DESCRIPTION
  Determines if identifier is present in BOOT_MISC_DETECT register to tell 
  SBL to enter the boot downloader, instead on continuing the normal boot 
  process.
  
DEPENDENCIES
  Data in BOOT_MISC_DETECT (or GCC_WIND_DOWN_TIMER for v1) is retained across a reset.
  
RETURN VALUE
  TRUE indicates downloader should be entered.

SIDE EFFECTS
  None

===========================================================================*/
boolean boot_dload_entry(void)
{
  /* Check to see if download ID is present. 
     For Bear family the cookie is now stored in the register BOOT_MISC_DETECT 
     and not IMEM.  This register is shared with PBL and maybe others.  Only
     one bit is needed and the mask SBL_BOOT_MISC_DETECT_MASK defines what
     section of the register SBL owns. */
  char dbg_info[40];
  uint32 dload_flag =0x0;
  boolean status = FALSE;
  
  do
  {
    dload_flag = HWIO_TCSR_TCSR_BOOT_MISC_DETECT_INM(SBL_DLOAD_MODE_BIT_MASK | SBL_MINIDUMP_MODE_BIT_MASK);
#ifdef QCLIB_IMAGE
	if (wmm_is_dload_mode_set())
	{
		dload_flag |= SBL_DLOAD_MODE_BIT_MASK;
	}
#endif
    boot_dload_flag_val = dload_flag;
    if (dload_flag)
    {
      snprintf(dbg_info, 40, "TCSR reg value 0x%x ", dload_flag);
      boot_log_message(dbg_info);
    
      /* Clear ID so the downloader is not entered again on the next boot. */
      HWIO_TCSR_TCSR_BOOT_MISC_DETECT_OUTM(SBL_DLOAD_MODE_BIT_MASK | SBL_MINIDUMP_MODE_BIT_MASK,0);      
#ifdef QCLIB_IMAGE
      wmm_clear_dload_cookie();
#endif
      status = TRUE;
      break;
    }
  }while(0);

  return status;

} /* boot_dload_entry() */

```


