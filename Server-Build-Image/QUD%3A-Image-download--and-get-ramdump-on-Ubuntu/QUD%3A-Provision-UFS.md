# Load prog_firehose_ddr.elf 
```
sudo ./fh_loader/QSaharaServer.bin -p "/dev/QTI_HS-USB_QDLoader_9008_1-5:1.0" -s 13:./fh_loader/prog_firehose_ddr.elf
```

# Provision UFS
```
tingkuanyu@TonyYuLinux1:/D/c1/11/images/image_sfpd_test/multi_flash_script/c1-11-developer-edl-2021.428.13$ sudo ./fh_loader/fh_loader.bin --port="/dev/QTI_HS-USB_QDLoader_9008_1-5:1.0" --search_path=./fh_loader/ --sendxml=./provision/provision_ufs31.xml --noprompt --showpercentagecomplete --zlpawarehost=0 --memoryname=ufs --setactivepartition=1

Base Version: 20.06.16.20.28
Binary build date: Apr 25 2021 @ 19:14:19
Incremental Build version: 21.04.25.19.14.19

16:22:01: INFO: 1. Calling fopen('.//port_trace.txt') with AccessMode='w'
16:22:01: INFO: FH_LOADER WAS CALLED EXACTLY LIKE THIS
************************************************
./fh_loader/fh_loader.bin --port=/dev/QTI_HS-USB_QDLoader_9008_1-5:1.0 --search_path=./fh_loader/ --sendxml=./provision/provision_ufs31.xml --noprompt --showpercentagecomplete --zlpawarehost=0 --memoryname=ufs --setactivepartition=1 
************************************************

16:22:01: INFO: Current working dir (cwd): /D/c1/11/images/image_sfpd_test/multi_flash_script/c1-11-developer-edl-2021.428.13/
16:22:01: INFO: Showing network mappings to allow debugging
16:22:01: INFO: './fh_loader/' changed to
16:22:01: INFO: this '/D/c1/11/images/image_sfpd_test/multi_flash_script/c1-11-developer-edl-2021.428.13/./fh_loader/'
16:22:01: INFO: 
:
16:22:01: INFO: TARGET SAID: 'INFO: Calling handler for ufs'
16:22:02: INFO: Response was success in running to unrecognized TAG (response)
16:22:02: INFO: Sending <setbootablestoragedrive>
16:22:02: INFO: Trying to write 93 bytes
16:22:02: INFO: Just wrote 93 bytes

16:22:02: INFO: TARGET SAID: 'INFO: Calling handler for setbootablestoragedrive'

16:22:02: INFO: TARGET SAID: 'INFO: Using scheme of value= 1'
16:22:02: INFO: ==============================================================
16:22:02: INFO: Files used and their paths
16:22:02: INFO:   1 './/port_trace.txt'
16:22:02: INFO:   2 './provision/provision_ufs31.xml'

16:22:02: INFO:      _             (done)
16:22:02: INFO:     | |                 
16:22:02: INFO:   __| | ___  _ __   ___ 
16:22:02: INFO:  / _` |/ _ \| '_ \ / _ \
16:22:02: INFO: | (_| | (_) | | | |  __/
16:22:02: INFO:  \__,_|\___/|_| |_|\___|
16:22:02: INFO: {All Finished Successfully}
:
```