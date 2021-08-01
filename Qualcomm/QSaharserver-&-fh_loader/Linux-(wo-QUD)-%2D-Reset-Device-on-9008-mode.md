# on Linux
## 1. load prog_firehose_ddr.elf by QSaharaServer
```
sudo ./QSaharaServer.bin -p /dev/ttyUSB0 -s 13:./prog_firehose_ddr.elf

bsp@bsp-build-server:/media/bsp/disk3/tonyyu/images/c1-11-developer-edl-2021.428.13/fh_loader$ sudo ./QSaharaServer.bin -p /dev/ttyUSB0 -s 13:./prog_firehose_ddr.elf
Binary build date: Apr 25 2021 @ 19:14:21
QSAHARASERVER CALLED LIKE THIS: './QSaharaServer.bi'Current working dir: /media/bsp/disk3/tonyyu/images/c1-11-developer-edl-2021.428.13/fh_loader
Sahara mappings:
2: amss.mbn
6: apps.mbn
8: dsp1.mbn
10: dbl.mbn
11: osbl.mbn
12: dsp2.mbn
16: efs1.mbn
17: efs2.mbn
20: efs3.mbn
21: sbl1.mbn
22: sbl2.mbn
23: rpm.mbn
25: tz.mbn
28: dsp3.mbn
29: acdb.mbn
30: wdt.mbn
31: mba.mbn
13: ./prog_firehose_ddr.elf
Requested ID 13, file: "/media/bsp/disk3/tonyyu/images/c1-11-developer-edl-2021.428.13/fh_loader/./prog_firehose_ddr.elf"
1026160 bytes transferred in 0.188475 seconds (5.1923MBps)


File transferred successfully


Sahara protocol completed
```


```
sudo ./fh_loader.bin --memoryname=ufs --port=/dev/ttyUSB0 --getstorageinfo=65210 | grep -i "Device Serial Number"

bsp@bsp-build-server:/media/bsp/disk3/tonyyu/images/c1-11-developer-edl-2021.428.13/fh_loader$ sudo ./fh_loader.bin --memoryname=ufs --port=/dev/ttyUSB0 --getstorageinfo=65210 | grep -i "Device Serial Number"
15:32:06: INFO: TARGET SAID: 'INFO: Device Serial Number: 0x58494120'
```

```
sudo ./fh_loader.bin --port=/dev/ttyUSB0 --reset

bsp@bsp-build-server:/media/bsp/disk3/tonyyu/images/c1-11-developer-edl-2021.428.13/fh_loader$ sudo ./fh_loader.bin --port=/dev/ttyUSB0 --reset

Base Version: 20.06.16.20.28
Binary build date: Apr 25 2021 @ 19:14:19
Incremental Build version: 21.04.25.19.14.19

15:32:39: INFO: 1. Calling fopen('.//port_trace.txt') with AccessMode='w'
15:32:39: INFO: FH_LOADER WAS CALLED EXACTLY LIKE THIS
************************************************
./fh_loader.bin --port=/dev/ttyUSB0 --reset 
************************************************

15:32:39: INFO: Current working dir (cwd): /media/bsp/disk3/tonyyu/images/c1-11-developer-edl-2021.428.13/fh_loader/
15:32:39: INFO: Showing network mappings to allow debugging


                                 (_)            
        __      ____ _ _ __ _ __  _ _ __   __ _ 
        \ \ /\ / / _` | '__| '_ \| | '_ \ / _` |
         \ V  V / (_| | |  | | | | | | | | (_| |
          \_/\_/ \__,_|_|  |_| |_|_|_| |_|\__, |
                                           __/ |
                                          |___/ 


15:32:39: WARNING: --reset parameter is deprecated and scheduled to be removed
15:32:39: INFO: User wants to talk to port '/dev/ttyUSB0'
15:32:39: INFO: Took       0.00006200 seconds to open port
15:32:39: INFO: Sorting TAGS to ensure order is <configure>,<erase>, others, <patch>,<power>
15:32:39: INFO: Sending <configure>
15:32:39: INFO: Trying to write 228 bytes
15:32:39: INFO: Just wrote 228 bytes

15:32:39: INFO: TARGET SAID: 'INFO: Calling handler for configure'

15:32:39: INFO: TARGET SAID: 'INFO: Storage type set to value eMMC'
15:32:39: INFO: fh.attrs.MaxPayloadSizeToTargetInBytes = 1048576
15:32:39: INFO: fh.attrs.MaxPayloadSizeToTargetInBytesSupported = 1048576
15:32:39: INFO: Sending <power>
15:32:39: INFO: Trying to write 99 bytes
15:32:39: INFO: Just wrote 99 bytes

15:32:39: INFO: TARGET SAID: 'INFO: Calling handler for power'

15:32:39: INFO: TARGET SAID: 'INFO: Will issue reset/power off 10000000 useconds, if this hangs check if watchdog is enabled'

15:32:39: INFO: TARGET SAID: 'INFO: bsp_target_reset() 1'
15:32:39: INFO: ==============================================================
15:32:39: INFO: Files used and their paths
15:32:39: INFO:   1 './/port_trace.txt'



                                 (_)            
        __      ____ _ _ __ _ __  _ _ __   __ _ 
        \ \ /\ / / _` | '__| '_ \| | '_ \ / _` |
         \ V  V / (_| | |  | | | | | | | | (_| |
          \_/\_/ \__,_|_|  |_| |_|_|_| |_|\__, |
                                           __/ |
                                          |___/ 


15:32:39: INFO: ==============================================================
15:32:39: INFO: NOTE: There were WARNINGS!! Repeated here, but please see log for more detail
--reset parameter is deprecated and scheduled to be removed
NOTE: There were WARNINGS!! Repeated above, but please see log for more detail



15:32:39: INFO: ==============================================================
15:32:39: INFO:      _             (done)
15:32:39: INFO:     | |                 
15:32:39: INFO:   __| | ___  _ __   ___ 
15:32:39: INFO:  / _` |/ _ \| '_ \ / _ \
15:32:39: INFO: | (_| | (_) | | | |  __/
15:32:39: INFO:  \__,_|\___/|_| |_|\___|
15:32:39: INFO: {All Finished Successfully}

15:32:39: INFO: Overall to target  0.002 seconds (0.00 Bps)

Writing log to '/media/bsp/disk3/tonyyu/images/c1-11-developer-edl-2021.428.13/fh_loader/port_trace.txt', might take a minute


Log is '/media/bsp/disk3/tonyyu/images/c1-11-developer-edl-2021.428.13/fh_loader/port_trace.txt'
```

# on Windows

## 1. load prog_firehose_ddr.elf by QSaharaServer
```
c:\VBShare\images\c1-11-developer-edl-2021.427.1\fh_loader>QSaharaServer.exe -p \\.\COM25 -s 13:prog_firehose_ddr.elf
Binary build date: Sep  7 2018 @ 20:25:00
QSAHARASERVER CALLED LIKE THIS: 'QSaharaServer.ex'Current working dir: c:\VBShare\images\c1-11-developer-edl-2021.427.1\fh_loader
Sahara mappings:
2: amss.mbn
6: apps.mbn
8: dsp1.mbn
10: dbl.mbn
11: osbl.mbn
12: dsp2.mbn
16: efs1.mbn
17: efs2.mbn
20: efs3.mbn
21: sbl1.mbn
22: sbl2.mbn
23: rpm.mbn
25: tz.mbn
28: dsp3.mbn
29: acdb.mbn
30: wdt.mbn
31: mba.mbn
13: prog_firehose_ddr.elf

17:37:28: Requested ID 13, file: "c:\VBShare\images\c1-11-developer-edl-2021.427.1\fh_loader\prog_firehose_ddr.elf"

17:37:28: 1026160 bytes transferred in 0.140000 seconds (6.9902MBps)



17:37:28: File transferred successfully



17:37:28: Sahara protocol completed
```
## 2. use fh_loader to reset device
```
c:\VBShare\images\c1-11-developer-edl-2021.427.1\fh_loader>fh_loader.exe --port=\\.\COM25 --reset

Base Version: 20.06.16.20.28
Binary build date: Dec 31 2020 @ 16:16:59
Incremental Build version: 20.12.31.16.16.59

17:37:35: INFO: 1. Calling fopen('.//port_trace.txt') with AccessMode='w'
17:37:35: INFO: FH_LOADER WAS CALLED EXACTLY LIKE THIS
************************************************
fh_loader.exe --port=\\.\COM25 --reset
************************************************

17:37:35: INFO: Current working dir (cwd): c:\VBShare\images\c1-11-developer-edl-2021.427.1\fh_loader\
17:37:35: INFO: Showing network mappings to allow debugging


                                 (_)
        __      ____ _ _ __ _ __  _ _ __   __ _
        \ \ /\ / / _` | '__| '_ \| | '_ \ / _` |
         \ V  V / (_| | |  | | | | | | | | (_| |
          \_/\_/ \__,_|_|  |_| |_|_|_| |_|\__, |
                                           __/ |
                                          |___/


17:37:35: WARNING: --reset parameter is deprecated and scheduled to be removed
17:37:35: INFO: User wants to talk to port '\\.\COM25'
17:37:35: INFO: Took       0.00000000 seconds to open port
17:37:35: INFO: Sorting TAGS to ensure order is <configure>,<erase>, others, <patch>,<power>
17:37:35: INFO: Sending <configure>

17:37:35: INFO: TARGET SAID: 'INFO: getsha256digest'

17:37:35: INFO: TARGET SAID: 'INFO: getUnlockBlob'

17:37:35: INFO: TARGET SAID: 'INFO: unlockVIP'

17:37:35: INFO: TARGET SAID: 'INFO: End of supported functions 17'

17:37:35: INFO: TARGET SAID: 'INFO: Calling handler for configure'

17:37:35: INFO: TARGET SAID: 'INFO: Storage type set to value eMMC'
17:37:35: INFO: fh.attrs.MaxPayloadSizeToTargetInBytes = 1048576
17:37:35: INFO: fh.attrs.MaxPayloadSizeToTargetInBytesSupported = 1048576
17:37:35: INFO: Sending <power>

17:37:35: INFO: TARGET SAID: 'INFO: Calling handler for power'

17:37:35: INFO: TARGET SAID: 'INFO: Will issue reset/power off 10000000 useconds, if this hangs check if watchdog is enabled'

17:37:35: INFO: TARGET SAID: 'INFO: bsp_target_reset() 1'
17:37:35: INFO: ==============================================================
17:37:35: INFO: Files used and their paths
17:37:35: INFO:   1 './/port_trace.txt'



                                 (_)
        __      ____ _ _ __ _ __  _ _ __   __ _
        \ \ /\ / / _` | '__| '_ \| | '_ \ / _` |
         \ V  V / (_| | |  | | | | | | | | (_| |
          \_/\_/ \__,_|_|  |_| |_|_|_| |_|\__, |
                                           __/ |
                                          |___/


17:37:35: INFO: ==============================================================
17:37:35: INFO: NOTE: There were WARNINGS!! Repeated here, but please see log for more detail
--reset parameter is deprecated and scheduled to be removed
NOTE: There were WARNINGS!! Repeated above, but please see log for more detail



17:37:35: INFO: ==============================================================
17:37:35: INFO:      _             (done)
17:37:35: INFO:     | |
17:37:35: INFO:   __| | ___  _ __   ___
17:37:35: INFO:  / _` |/ _ \| '_ \ / _ \
17:37:35: INFO: | (_| | (_) | | | |  __/
17:37:35: INFO:  \__,_|\___/|_| |_|\___|
17:37:35: INFO: {All Finished Successfully}

17:37:35: INFO: Overall to target  0.063 seconds (0.00 Bps)

Writing log to 'c:\VBShare\images\c1-11-developer-edl-2021.427.1\fh_loader\port_trace.txt', might take a minute


Log is 'c:\VBShare\images\c1-11-developer-edl-2021.427.1\fh_loader\port_trace.txt'
```