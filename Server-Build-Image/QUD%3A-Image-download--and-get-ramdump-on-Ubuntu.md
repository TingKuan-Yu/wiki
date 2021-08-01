# Topic
- QUD: Get Ramdump
- QUD: EDL Flash Bootloader
- QUD: Provision UFS
- QUD: EDL Get UFS Serial Number
- Build fh_loader and QSaharaServer for Linux host

# QUD installation
## If running into QUD issue, please reinstall the driver and then reboot host pc.
  - reference: KBA-201209020550 PCAT & QUTS on Linux deployment guideline

## Login QPM

```
$ qpm-cli --login <user-name>
Password: ***************
```

## Check if a user have access to the QUD, QUTS and PCAT tools.
```
$ qpm-cli --product-list
```

## Activate QUD, QUTS and PCAT licenses
```
$ qpm-cli --license-activate qud
$ qpm-cli --license-activate quts
$ qpm-cli --license-activate pcat
```

## Install QUD, QUTS and PCAT
```
$ qpm-cli --install qud
$ qpm-cli --install quts
$ qpm-cli --install pcat
```

## Device validation for PCAT
```
Check the driver lists of Qualcomm devices
$ ls –la /dev/Q*
crw-rw-rw- 1 root root 242 0 Dec 10 10:51 /dev/QTI_HS-USB_QDLoader_9008_3-8:1.0
```