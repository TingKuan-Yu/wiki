# only on  ubuntu 18.04 not for 20.04

# Without QUD 
## /dev/serial/by-id/usb-Qualcomm_CDMA_Technologies_MSM_QUSB_BULK_CID:041D_SN:0B31EA41-if00-port0
```
PS /home/tingkuanyu> Get-ChildItem /dev/serial/by-id/usb-Qualcomm_CDMA_Technologies_MSM_QUSB_BULK_CID:041D_SN:0B31EA41-if00-port0

    Directory: /dev/serial/by-id

Mode                 LastWriteTime         Length Name
----                 -------------         ------ ----
l----           5/11/2021  2:09 PM             13 usb-Qualcomm_CDMA_Technologies_MSM_QUSB_BULK_CID:041D_SN:0B31EA41-if00-port0 -> /dev/ttyUSB4
```
```
tingkuanyu@TKubunt20:~$ ls /dev/serial/by-path/* -1
/dev/serial/by-path/pci-0000:00:14.0-usb-0:5:1.0-port0
/dev/serial/by-path/pci-0000:00:14.0-usb-0:6:1.0-port0
/dev/serial/by-path/pci-0000:00:14.0-usb-0:6:1.1-port0
/dev/serial/by-path/pci-0000:00:14.0-usb-0:6:1.2-port0
/dev/serial/by-path/pci-0000:00:14.0-usb-0:6:1.3-port0
tingkuanyu@TKubunt20:~$ ls /dev/serial/by-id/* -1
/dev/serial/by-id/usb-FTDI_Yoda_v2.0_LP5B5806-if00-port0
/dev/serial/by-id/usb-FTDI_Yoda_v2.0_LP5B5806-if01-port0
/dev/serial/by-id/usb-FTDI_Yoda_v2.0_LP5B5806-if02-port0
/dev/serial/by-id/usb-FTDI_Yoda_v2.0_LP5B5806-if03-port0
/dev/serial/by-id/usb-Qualcomm_CDMA_Technologies_MSM_QUSB_BULK_CID:041D_SN:0B31EA41-if00-port0
tingkuanyu@TKubunt20:~$ ls /dev/ttyUSB* -1
/dev/ttyUSB0
/dev/ttyUSB1
/dev/ttyUSB2
/dev/ttyUSB3
/dev/ttyUSB4
```

# With QUD
```
PS /home/tingkuanyu> Get-ChildItem /dev/QTI_HS-USB_QDLoader_9008_1-5:1.0 

    Directory: /dev

Mode                 LastWriteTime         Length Name
----                 -------------         ------ ----
-----           5/11/2021  2:38 PM              0 QTI_HS-USB_QDLoader_9008_1-5:1.0
```