[[_TOC_]]


# QC documents
  - Get MSM_ID or SERIAL NUMBER from MSM chips
   - KBA-170315075349

# There few methods to get MSM SOC serial number
## 1. Uart log of XBL
Chip Serial Number : 0xB31EA41

## 2. EDL method
- EDL Mode Operation - Overview (azure.com) 
  - How to Get SOC Serial number under EDL mode 
    https://dev.azure.com/E-OS/device/_wiki/wikis/Wiki/168515/EDL-Mode-Operation

## 3. Fastboot command
- There is no fastboot command supports getting SOC serial number now. However, I can add a new method in ABL. 
  - Patch is ready here https://dev.azure.com/E-OS/device/_git/caf-abl.tianocore.edk2/commit/befad2d65417ef6c4f84c6704f1e500c6a2baae3?refName=refs%2Fheads%2Fbsp_tony_abl_dev1 .
- Example
```
C:\VBShare>adb reboot bootloader
C:\VBShare>fastboot oem get-soc-serial
(bootloader) SOC Serial Number: 0xB31EA41

OKAY [  0.005s]
Finished. Total time: 0.006s
```

## 4. adb command to get soc serial
```
c1:/ $ cat /sys/devices/soc0/serial_number
187820609
c1:/ $ '{0:X8}' -f 187820609
127|c1:/ $ exit
PS C:\Users\tingkuanyu\Zeta> '{0:X8}' -f 187820609
0B31EA41
```


# XBL Code Study for Uart Log: Chip Serial Number : **0xB31EA41**
- HWIO_INF(CHIPINFO_SERIAL_NUM_REG, SERIAL_NUM)
  - read from HWIO_SERIAL_NUM_ADDR and shift HWIO_SERIAL_NUM_SERIAL_NUM_SHFT
- This is the serial number of SOC.
  - Look up HW Register of SM8350
    https://docviewer.qualcomm.com/hrd/HRD-SM8350-S
- The source code to get SOC serial number is from below snippet. However, the register 0x00786134 is unable to check from https://docviewer.qualcomm.com/hrd/HRD-SM8350-S.

```
QcomPkg/SocPkg/Lahaina/Include/msmhwiobase.h:
#define SECURITY_CONTROL_BASE                                       0x00780000

QcomPkg/SocPkg/Lahaina/Include/ChipInfoHWIO.h
#define SECURITY_CONTROL_CORE_REG_BASE    (SECURITY_CONTROL_BASE      + 0x00000000)
#define HWIO_SERIAL_NUM_ADDR       (SECURITY_CONTROL_CORE_REG_BASE      + 0x00006134)
#define HWIO_SERIAL_NUM_INM(m)      \
        in_dword_masked(HWIO_SERIAL_NUM_ADDR, m)

#define HWIO_SERIAL_NUM_SERIAL_NUM_BMSK                           0xffffffff
#define HWIO_SERIAL_NUM_SERIAL_NUM_SHFT                           0x0

QcomPkg/Include/HALhwio.h:
#define __msmhwio_inm(hwiosym, mask)          HWIO_##hwiosym##_INM(mask)
#define __msmhwio_shft(hwiosym, hwiofldsym)   HWIO_##hwiosym##_##hwiofldsym##_SHFT

#define HWIO_SHFT(hwio_regsym, hwio_fldsym)              __msmhwio_shft(hwio_regsym, hwio_fldsym)
#define HWIO_INM(hwiosym, mask)               __msmhwio_inm(hwiosym, mask)
#define HWIO_INF(io, field)                   (HWIO_INM(io, HWIO_FMSK(io, field)) >> HWIO_SHFT(io, field))
```

```
QcomPkg/SocPkg/Lahaina/Include/ChipInfoHWIO.h:
#define CHIPINFO_SERIAL_NUM_REG           SERIAL_NUM

QcomPkg/Library/ChipInfoLib/ChipInfoLoader.c:
DALResult ChipInfo_Init
(
 void
)
  ChipInfoCtxt.nSerialNum           = HWIO_INF(CHIPINFO_SERIAL_NUM_REG, SERIAL_NUM);

```
```
QcomPkg/Library/ChipInfoLib/ChipInfo.c:
ChipInfoSerialNumType ChipInfo_GetSerialNumber(void)
{
  return ChipInfoCtxt.nSerialNum;
} /*  END ChipInfo_GetSerialNumber    */

QcomPkg/Library/ChipInfoLib/DalChipInfoFwk.c:

static DALResult
ChipInfo_DalChipInfo_GetSerialNumber(DalDeviceHandle * h, ChipInfoSerialNumType* pnSerialNum)
{
  *pnSerialNum = ChipInfo_GetSerialNumber();
  return DAL_SUCCESS;
}

static void
ChipInfo_InitInterface(ChipInfoClientCtxt* pclientCtxt)
{
  static const DalChipInfo vtbl = {
    :
    ChipInfo_DalChipInfo_GetSerialNumber,
    :
  };
  :
}

QcomPkg/Include/DDIChipInfo.h:
static __inline DALResult
DalChipInfo_GetSerialNumber(DalDeviceHandle * _h,  ChipInfoSerialNumType * pnSerialNum)
{
   return ((DalChipInfoHandle *)_h)->pVtbl->GetSerialNumber(_h, pnSerialNum);
}
```
- UEFI Chipset Information Driver
```
QcomPkg/Drivers/ChipInfoDxe/ChipInfoDxe.c:
static EFI_CHIPINFO_PROTOCOL ChipInfoProtocol =
{
  EFI_CHIPINFO_PROTOCOL_REVISION,
  :  
  EFI_DalChipInfo_GetSerialNumber,
  :
};

EFI_STATUS
EFI_DalChipInfo_GetSerialNumber(IN  EFI_CHIPINFO_PROTOCOL *This,
                               OUT EFIChipInfoSerialNumType *peId )
{
:
  if(chipInfoHandle)
  {
    result = DalChipInfo_GetSerialNumber(chipInfoHandle,(ChipInfoSerialNumType *) peId);
  }
:
} /* EFI_DalChipInfo_GetSerialNumber */
```
- Use EFI_CHIPINFO_PROTOCOL to get serial number.
```
QcomPkg/Library/PlatformBdsLib/PlatformBdsLib.c:
DisplayPlatformInfo (VOID)
  EFI_CHIPINFO_PROTOCOL               *pChipInfoProtocol;
  if ((Status = pChipInfoProtocol->GetSerialNumber(pChipInfoProtocol, 
                                                   &ChipSerialNum)) != EFI_SUCCESS)
    return Status;
      :

  DEBUG ((EFI_D_ERROR, "Chip Serial Number : 0x%x\n", ChipSerialNum));


```
