[[_TOC_]]


# SFPD Serial Number Overview
  - SFxxxxxxxxxxxx
```
C:\VBShare\c1-11-developer-edl-2021.412.12\fh_loader>adb devices
List of devices attached
SFF782A8CE2443  device

c1:/ # getprop ro.boot.serialno
SFF782A8CE2443

c1:/ # getprop ro.serialno
SFF782A8CE2443

C:\VBShare\c1-11-developer-edl-2021.412.12\fh_loader>fastboot devices
SFF782A8CE2443  fastboot

C:\VBShare\c1-11-developer-edl-2021.412.12\fh_loader>fastboot getvar serialno
serialno: SFF782A8CE2443
Finished. Total time: 0.003s
```

# ABL Code snippet
- Get serial number
  - GetBoardSerialNumFromSfpd()
```
Library/SfpdUtils/SfpdUtils.c:
#define SERIAL_NUM_FILE L"device\\SerialNumber.txt"
EFI_STATUS GetBoardSerialNumFromSfpd(CHAR8 *buffer, UINT32 bufferSize)
{
:

  status = pSfpdPartitionAccessProtocol->read_file_from_sfpd(pSfpdPartitionAccessProtocol,
                                                             SERIAL_NUM_FILE,
                                                             &tempBuffer,
                                                             &readSize);
:
}
```
  - if fail to use GetBoardSerialNumFromSfpd()
    - pMsManufacturingModeProtocol->GetSignatureChallenge()
```
Library/BootLib/Board.c:
EFI_STATUS
BoardSerialNum (CHAR8 *StrSerialNum, UINT32 Len)
{
:
 /* ==> MS changed */
  Status = GetBoardSerialNumFromSfpd(StrSerialNum, Len);
  if (!EFI_ERROR(Status)) {
    DEBUG ((EFI_D_INFO, "Get serial num from sfpd!\n"));
    return Status;
  }

  // Get random number if mounting sfpd partition fails or unable to read file
  DEBUG ((EFI_D_INFO, "[%a] Error: Unable to get serial number from file: sfpd...setting default serial number\n", __FUNCTION__));

  MS_MANUFACTURINGMODE_PROTOCOL *pMsManufacturingModeProtocol;

  Status = gBS->LocateProtocol (&gMsManufacturingModeProtocolGuid, NULL, (VOID **)&pMsManufacturingModeProtocol);
  if (EFI_ERROR (Status)) {
    DEBUG ((EFI_D_ERROR, "[%a] Locate Protocol failed for gMsManufacturingModeProtocolGuid\n", __FUNCTION__));
  }
  else {
    Status = pMsManufacturingModeProtocol->GetSignatureChallenge (pMsManufacturingModeProtocol, InvalidNum, MAX_SERIAL_NUM_LEN);
    if (EFI_ERROR (Status)) {
      DEBUG ((EFI_D_ERROR, "[%a] - Error getting signature challenge\n", __FUNCTION__));
    }
    else {
      // Invalid serial number: sfNNNNNNNNNNNN
      AsciiStrnCpyS (StrSerialNum, Len, Invalid_Prefix, AsciiStrLen(Invalid_Prefix));
      for (int i = 0; i < INVALID_SERIAL_NUM_LEN; i++) {
        AsciiSPrint (InvalidBuf, sizeof(CHAR8)*2, "%x", InvalidNum[i]);
        AsciiStrnCat (StrSerialNum, InvalidBuf, AsciiStrLen(InvalidBuf));
      }
      return EFI_SUCCESS;
    }
  }
  /* MS changed <== */
:
}
```
- Command line
```
Library/BootLib/UpdateCmdLine.c:
STATIC CONST CHAR8 *UsbSerialCmdLine = " androidboot.serialno=";
typedef struct UpdateCmdLineParamList {
:
  CHAR8 *StrSerialNum;
:
}

UpdateCmdLine (CONST CHAR8 *CmdLine,
               CHAR8 *FfbmStr,
               BOOLEAN Recovery,
               BOOLEAN AlarmBoot,
               CONST CHAR8 *VBCmdLine,
               CHAR8 **FinalCmdLine,
               UINT32 HeaderVersion)
{
:
  CHAR8 StrSerialNum[SERIAL_NUM_SIZE];

  Status = BoardSerialNum (StrSerialNum, sizeof (StrSerialNum));
:
  Param.StrSerialNum = StrSerialNum;
:
  Status = UpdateCmdLineParams (&Param, FinalCmdLine);
:
}
```
- fastboot
```
Library/FastbootLib/FastbootCmds.c:
    FastbootPublishVar ("serialno", StrSerialNum);
```

# XBL Code snippet




