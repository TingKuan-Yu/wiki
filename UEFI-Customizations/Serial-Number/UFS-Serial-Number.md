[[_TOC_]]

# Qualcomm Documents
 - Where does adb device's serial number come from?
   - KBA-180912014938

# Qualcomm default serial number is from UFS

## XBL Code snippet
  - product_serial_num: UFS serial - 2 bytes
```
QcomPkg/Drivers/UFSDxe/UFS.c
   rc = ufs_get_device_info_str (hUFS, info.iSerialNumber,
                                 serial_num_str, sizeof(serial_num_str));
   card_info->serial_num_len = serial_num_str[0] - 2;  // Get length and reduce by 2 bytes (length, IDN)

   CopyMem(card_info->product_serial_num, &serial_num_str[2], card_info->serial_num_len);
```
## ABL Code snippet
- StrSerial: CRC32 of product_serial_num
```
Library/BootLib/Board.c
EFI_STATUS
BoardSerialNum (CHAR8 *StrSerialNum, UINT32 Len)
      Status =
      gBS->HandleProtocol (HandleInfoList[0].Handle,
                           &gEfiMemCardInfoProtocolGuid, (VOID **)&CardInfo);
  if (Status != EFI_SUCCESS) {
    DEBUG ((EFI_D_ERROR, "Error locating MemCardInfoProtocol:%x\n", Status));
    return Status;
  }

  if (CardInfo->GetCardInfo (CardInfo, &CardInfoData) == EFI_SUCCESS) {
    if (Type == UFS) {
      Status = gBS->CalculateCrc32 (CardInfoData.product_serial_num,
                                    CardInfoData.serial_num_len, &SerialNo);
      if (Status != EFI_SUCCESS) {
        DEBUG ((EFI_D_ERROR,
                "Error calculating Crc of the unicode serial number: %x\n",
                Status));
        return Status;
      }
      AsciiSPrint (StrSerialNum, Len, "%x", SerialNo);
    } else {
      AsciiSPrint (StrSerialNum, Len, "%x",
                   *(UINT32 *)CardInfoData.product_serial_num);
    }

    /* adb is case sensitive, convert the serial number to lower case
     * to maintain uniformity across the system. */
    ToLower (StrSerialNum);
  }
```

# How to get UFS Serial number under EDL mode

## On Windows
- refer to Qualcomm KBA-160824075724 & 80-P6549-1
  - power on device to edl mode
  - Download prog_firehose_ddr.elf to device

```
C:\VBShare\c1-11-developer-edl-2021.412.12\fh_loader>QSaharaServer.exe -p \\.\COM25 -s 13:prog_firehose_ddr.elf
Binary build date: Sep  7 2018 @ 20:25:00
QSAHARASERVER CALLED LIKE THIS: 'QSaharaServer.ex'Current working dir: C:\VBShare\c1-11-developer-edl-2021.412.12\fh_loader
Sahara mappings:
:
13: prog_firehose_ddr.elf

18:09:37: Requested ID 13, file: "C:\VBShare\c1-11-developer-edl-2021.412.12\fh_loader\prog_firehose_ddr.elf"

18:09:37: 1026160 bytes transferred in 0.140000 seconds (6.9902MBps)

18:09:37: File transferred successfully

18:09:37: Sahara protocol completed
```
- use fh_loader.exe to get ufs serial number
  - For my device, it is "Serial Number: 0x58494120".
```
C:\VBShare\c1-11-developer-edl-2021.412.12\fh_loader>fh_loader.exe --memoryname=ufs --port=\\.\COM25 --getstorageinfo=65210

Base Version: 20.06.16.20.28
Binary build date: Dec 31 2020 @ 16:16:59
Incremental Build version: 20.12.31.16.16.59

18:09:55: INFO: 1. Calling fopen('.//port_trace.txt') with AccessMode='w'
18:09:55: INFO: FH_LOADER WAS CALLED EXACTLY LIKE THIS
************************************************
fh_loader.exe --memoryname=ufs --port=\\.\COM25 --getstorageinfo=65210
************************************************
:
18:09:55: INFO: TARGET SAID: 'INFO: Device Serial Number: 0x58494120'
:
```



## On Linux
- load prog_firehose_ddr.elf by QSaharaServer.bin
```
sudo ./QSaharaServer.bin -p /dev/ttyUSB0 -s 13:./prog_firehose_ddr.elf

bsp@bsp-build-server:/media/bsp/disk3/tonyyu/images/c1-11-developer-edl-2021.428.13/fh_loader$ sudo ./QSaharaServer.bin -p /dev/ttyUSB0 -s 13:./prog_firehose_ddr.elf
Binary build date: Apr 25 2021 @ 19:14:21
QSAHARASERVER CALLED LIKE THIS: './QSaharaServer.bi'Current working dir: /media/bsp/disk3/tonyyu/images/c1-11-developer-edl-2021.428.13/fh_loader
Sahara mappings:
:
13: ./prog_firehose_ddr.elf
Requested ID 13, file: "/media/bsp/disk3/tonyyu/images/c1-11-developer-edl-2021.428.13/fh_loader/./prog_firehose_ddr.elf"
1026160 bytes transferred in 0.188475 seconds (5.1923MBps)

File transferred successfully

Sahara protocol completed
```

- get UFS serial number by fh_loader.bin
```
bsp@bsp-build-server:/media/bsp/disk3/tonyyu/images/c1-11-developer-edl-2021.428.13/fh_loader$ sudo ./fh_loader.bin --memoryname=ufs --port=/dev/ttyUSB0 --getstorageinfo=65210 | grep -i "Device Serial Number"
15:32:06: INFO: TARGET SAID: 'INFO: Device Serial Number: 0x58494120'
```
