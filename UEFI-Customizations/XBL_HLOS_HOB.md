# Overview
- Reference
  - boot/Sm8350FamilyPkg/Include/XblHlosHob.h
- **Acronym** Expansion:
  - **XBL**: "X-Boot Loader": Qualcomm's name for SBL and UEFI-based bootloader/firmware blob
  - **HLOS**: "High-Level Operating system": Refers to high level operating system boot strapped by XBL
  - **Hob**: "Handoff Block": Refers to the 100 bytes of OEM space allocated in IMEM in Target_cust.h
     where this structure is meant to be stored
- **layout** definition of the shared communication structure between different modules in XBL and OS. 
  - The start address of this layout is SHARED_IMEM_OEM_BASE and it is **SHARED_IMEM_OEM_SIZE** 

# Memory Map
- boot/QcomPkg/SocPkg/Include/Soc_cust.h
  - #define SHARED_IMEM_OEM_SIZE             100
- KBA-210406224130


# Related Tasks
- https://dev.azure.com/E-OS/Zeta/_workitems/edit/103407

# Related PRs
- https://dev.azure.com/E-OS/device/_git/qcom-BOOT.MXF.1.0-premium-high-2020-spf-1-0_amss_standard_oem/commit/7ae03a1a67e134c937ea5883f7a6bbf9890ea7cd?refName=refs%2Fheads%2Fc1%2F11%2Fmain&path=%2Fboot_images%2Fboot%2FQcomPkg%2FSocPkg%2FLahaina%2FCommon%2Fuefiplat.cfg


# boot/Sm8350FamilyPkg/Include/XblHlosHob.h
```
//
// Note1: The following structure is a packed structure
// Note2: We need to match the definitions here with the offsets defined in the os side header file
// Note3: A limited amount of memory is reserved for OEMs. So if a big structure needs to be communicated
// please allocate a run-time memory buffer in UEFI and then store the pointer to it in this area. 
//
#pragma pack (1)
typedef struct ccccc
{
    UINT8 BoardID;                          // (00)
    UINT8 BatteryPresent;                   // (01) Indicates battery presence: 0 - battery absent, 1 - battery present
    UINT8 HwInitRetries;                    // (02) Indicates retries attempted to initialize descrete hardware circuit
    UINT8 IsCustomerMode;                   // (03) Indicates whether the device is in Manufacturing Mode: 0 - not in manuf mode, 1 - in manuf mode
    UINT8 ActMode;                          // (04) Indicates if the ACT mode is enabled (used to run checks and put device to shipmode at factory) 0 - ACT disabled 1- ACT enabled.
    UINT8 PmicResetReason;                  // (05) PmicResetReason: 9 - battery driver triggered
    CHAR8 TouchFWVersion[MAX_VERSION_LEN];  // (06) Current Touch Firmware version number
    UINT16 OCPErrorLocation;                // (07) Identify which power rail has the OCP Error
                                                  //      Bit(s)     Meaning
                                                  //      15         More than one OCP error occurred
                                                  //      14-12      PMIC
                                                  //      11-7       SMPS
                                                  //      6-2        LDO
                                                  //      1-0        BOB
    UINT8 IsRaflaMode;                      // (08) Indicates whether the device is in Rafla Mode: 0 - not in Rafla mode, 1 - in Rafla mode
    UINT8 DisplayRDID[DISPLAY_RDID_LEN];    // (09) Indicates which TDM RDID has been read.
                                                  //Index 0 is related to manufacturer, LGD--, Here we will see 0x81 for Zeta
                                                  //Index 1 is related to TDM version, EV1, EV2, EV3, DV, MP etc
                                                  // 0         - Unknown TDM, we have bigger problems.
                                                  // 0x31-0x3F - EV2
                                                  // 0x41-0x4F - EV3
                                                  //Index 2 tells us which one we read, left side or right side, we will mstly see left side
                                                  //0x9        - Left side
                                                  //0x10       - right side
} XBL_HLOS_HOB, *PXBL_HLOS_HOB; 
#pragma pack ()
```

# boot/Sm8350FamilyPkg/Library/XblHlosHobLib/XblHlosHobLib.c
```
/*===========================================================================

FUNCTION GET_XBLHLOSHOB_POINTER

DESCRIPTION
	Returns a pointer to the XBL HLOS HOB structure in IMEM

RETURN VALUE
	TRUE on success, FALSE on failure

===========================================================================*/
PXBL_HLOS_HOB get_xblhloshob_pointer(void)
{ 
    PXBL_HOB_HANDOVER_STATUS handover = (PXBL_HOB_HANDOVER_STATUS)SHARED_IMEM_OEM_BASE;
	if(handover->DDRHobInitialized)
        return (PXBL_HLOS_HOB)FixedPcdGet64(PcdAppsHobPointer);
    else
        return (PXBL_HLOS_HOB)(SHARED_IMEM_OEM_BASE+sizeof(XBL_HOB_HANDOVER_STATUS));
}


```




