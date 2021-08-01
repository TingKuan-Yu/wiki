# Load prog_firehose_ddr.elf 
```
tingkuanyu@TonyYuLinux1:/D/c1/11/images/image_sfpd_test/multi_flash_script/c1-11-developer-edl-2021.428.13$ sudo ./fh_loader/QSaharaServer.bin -p "/dev/QTI_HS-USB_QDLoader_9008_1-5:1.0" -s 13:./fh_loader/prog_firehose_ddr.elf
[sudo] password for tingkuanyu: 
Binary build date: Apr 25 2021 @ 19:14:21
QSAHARASERVER CALLED LIKE THIS: './fh_loader/QSaharaServer.bi'Current working dir: /D/c1/11/images/image_sfpd_test/multi_flash_script/c1-11-developer-edl-2021.428.13
Sahara mappings:

:

13: ./fh_loader/prog_firehose_ddr.elf
Requested ID 13, file: "/D/c1/11/images/image_sfpd_test/multi_flash_script/c1-11-developer-edl-2021.428.13/./fh_loader/prog_firehose_ddr.elf"
1026160 bytes transferred in 0.142285 seconds (6.8779MBps)

File transferred successfully

Sahara protocol completed
```

# Get UFS serial number
```
tingkuanyu@TonyYuLinux1:/D/c1/11/images/image_sfpd_test/multi_flash_script/c1-11-developer-edl-2021.428.13$ sudo ./fh_loader/fh_loader.bin --memoryname=ufs --port="/dev/QTI_HS-USB_QDLoader_9008_1-5:1.0" --getstorageinfo=65210 --reset | grep -i "Device Serial Number"
14:15:44: INFO: TARGET SAID: 'INFO: Device Serial Number: 0x58494120'
```
