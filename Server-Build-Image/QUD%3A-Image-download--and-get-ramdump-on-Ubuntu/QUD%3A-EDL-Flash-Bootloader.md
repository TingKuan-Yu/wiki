
# Load prog_firehose_ddr.elf 
```
sudo ./fh_loader/QSaharaServer.bin -p "/dev/QTI_HS-USB_QDLoader_9008_1-5:1.0" -s 13:./fh_loader/prog_firehose_ddr.elf
```

# Flash bootloader by fh_loader.bin
```
tingkuanyu@TonyYuLinux1:/D/c1/11/images/image_sfpd_test/multi_flash_script/c1-11-developer-edl-2021.428.13$ sudo ./fh_loader/fh_loader.bin --port="/dev/QTI_HS-USB_QDLoader_9008_1-5:1.0" --search_path=bin/ --sendxml=./xml/rawprogram1.xml,./xml/rawprogram4.xml,./xml/rawprogram3.xml --noprompt --zlpawarehost=0 --memoryname=ufs --setactivepartition=1
:
16:30:39: INFO:  25 '/D/c1/11/images/image_sfpd_test/multi_flash_script/c1-11-developer-edl-2021.428.13/bin/sec.elf'
16:30:39: INFO:  26 '/D/c1/11/images/image_sfpd_test/multi_flash_script/c1-11-developer-edl-2021.428.13/bin/spunvm.bin'
16:30:39: INFO:  27 '/D/c1/11/images/image_sfpd_test/multi_flash_script/c1-11-developer-edl-2021.428.13/bin/gpt_main4.bin'
16:30:39: INFO:  28 '/D/c1/11/images/image_sfpd_test/multi_flash_script/c1-11-developer-edl-2021.428.13/bin/gpt_backup4.bin'
16:30:39: INFO:  29 '/D/c1/11/images/image_sfpd_test/multi_flash_script/c1-11-developer-edl-2021.428.13/bin/gpt_main3.bin'
16:30:39: INFO:  30 '/D/c1/11/images/image_sfpd_test/multi_flash_script/c1-11-developer-edl-2021.428.13/bin/gpt_backup3.bin'

16:30:39: INFO:      _             (done)
16:30:39: INFO:     | |                 
16:30:39: INFO:   __| | ___  _ __   ___ 
16:30:39: INFO:  / _` |/ _ \| '_ \ / _ \
16:30:39: INFO: | (_| | (_) | | | |  __/
16:30:39: INFO:  \__,_|\___/|_| |_|\___|
16:30:39: INFO: {All Finished Successfully}

16:30:39: INFO: Overall to target  5.017 seconds (40.77 MBps)
:

```
