# Reference
- QC doc: 80-P6549-3 Rev. A
  - 2.5 Capture RAM dump with QSaharaserver
  
# method
- RAM dump can also be captured by QSaharserver, which locates at C:\Program Files (x86)\Qualcomm\QPST\bin. Here are the steps: 
   - 1.Connect a crash device to the PC. 
   - 2.Run the following command line to capture RAM dump. 
     - QSaharserver -u [PORT_NUM] -m -w [PATH_TO_SAVE_RAMP_DUMP]
     - For example
       - QSaharserver -u 38 -m -w c:\VBShare\images\c1-11-developer-edl-2021.427.1\fh_loader\ramdump
# Rractice on Windows
## trigger panic
```
c:\VBShare\images\c1-11-developer-edl-2021.427.1\fh_loader>adb root
restarting adbd as root

c:\VBShare\images\c1-11-developer-edl-2021.427.1\fh_loader>adb shell
c1:/ # cd /proc/
c1:/proc # echo c > sysrq-trigger
```

## use QSaharserver to get ramdump
```
c:\VBShare\images\c1-11-developer-edl-2021.427.1\fh_loader>QSaharaServer.exe -u 38 -m -w C:\VBShare\images\c1-11-developer-edl-2021.427.1\fh_loader\ramdump\
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

18:44:12: Received file 'load.cmm'

18:44:12: 3480 bytes transferred in 0.000000 seconds

18:44:12: File transferred successfully



18:44:57: Received file 'DDRCS0_3.BIN'

18:44:57: -2147483648 bytes transferred in 45.734000 seconds (44.7807MBps)



18:44:57: File transferred successfully



18:45:44: Received file 'DDRCS0_2.BIN'

18:45:44: -2147483648 bytes transferred in 46.281000 seconds (44.2514MBps)



18:45:44: File transferred successfully



18:46:30: Received file 'DDRCS0_1.BIN'

18:46:30: -2147483648 bytes transferred in 46.062000 seconds (44.4618MBps)



18:46:30: File transferred successfully



18:47:16: Received file 'DDRCS0_0.BIN'

18:47:16: -2147483648 bytes transferred in 45.984000 seconds (44.5372MBps)



18:47:16: File transferred successfully



18:47:16: Received file 'DBG_EN.BIN'

18:47:16: 4 bytes transferred in 0.000000 seconds

18:47:16: File transferred successfully



18:47:16: Received file 'FSM_CTRL.BIN'

18:47:16: 4 bytes transferred in 0.000000 seconds

18:47:16: File transferred successfully



18:47:16: Received file 'FSM_STS.BIN'

18:47:16: 4 bytes transferred in 0.000000 seconds

18:47:16: File transferred successfully



18:47:16: Received file 'PIMEM.BIN'

18:47:16: 12582912 bytes transferred in 0.281000 seconds (42.7046MBps)



18:47:16: File transferred successfully



18:47:16: Received file 'DDR_DATA.BIN'

18:47:16: 32768 bytes transferred in 0.016000 seconds (1.9531MBps)



18:47:16: File transferred successfully



18:47:16: Received file 'RST_STAT.BIN'

18:47:16: 4 bytes transferred in 0.015000 seconds (0.0003MBps)



18:47:16: File transferred successfully



18:47:16: Received file 'sbl_pmic_dump.bin'

18:47:16: 524288 bytes transferred in 0.219000 seconds (2.2831MBps)



18:47:16: File transferred successfully



18:47:16: Received file 'PMON_HIS.BIN'

18:47:16: 400 bytes transferred in 0.016000 seconds (0.0238MBps)



18:47:16: File transferred successfully



18:47:16: Received file 'PMIC_PON.BIN'

18:47:16: 8 bytes transferred in 0.000000 seconds

18:47:16: File transferred successfully



18:47:16: Received file 'IPA_SEQ.BIN'

18:47:16: 968 bytes transferred in 0.016000 seconds (0.0577MBps)



18:47:16: File transferred successfully



18:47:16: Received file 'IPA_GSI.BIN'

18:47:16: 7680 bytes transferred in 0.016000 seconds (0.4578MBps)



18:47:16: File transferred successfully



18:47:16: Received file 'IPA_MBOX.BIN'

18:47:16: 256 bytes transferred in 0.000000 seconds

18:47:16: File transferred successfully



18:47:17: Received file 'IPA_HRAM.BIN'

18:47:17: 102400 bytes transferred in 0.015000 seconds (6.5104MBps)



18:47:17: File transferred successfully



18:47:17: Received file 'IPA_SRAM.BIN'

18:47:17: 19232 bytes transferred in 0.016000 seconds (1.1463MBps)



18:47:17: File transferred successfully



18:47:17: Received file 'IPA_IU.BIN'

18:47:17: 40704 bytes transferred in 0.000000 seconds

18:47:17: File transferred successfully



18:47:17: Received file 'CD_SHIMM.BIN'

18:47:17: 4096 bytes transferred in 0.000000 seconds

18:47:17: File transferred successfully



18:47:17: Received file 'CD_BTIMM.BIN'

18:47:17: 1572864 bytes transferred in 0.031000 seconds (48.3871MBps)



18:47:17: File transferred successfully



18:47:17: Received file 'CD_BTDDR.BIN'

18:47:17: 1044480 bytes transferred in 0.015000 seconds (66.4063MBps)



18:47:17: File transferred successfully



18:47:17: Received file 'CD_STRCT.BIN'

18:47:17: 496 bytes transferred in 0.016000 seconds (0.0296MBps)



18:47:17: File transferred successfully



18:47:17: Received file 'DCC_CFG.BIN'

18:47:17: 4096 bytes transferred in 0.000000 seconds

18:47:17: File transferred successfully



18:47:17: Received file 'DCC_SRAM.BIN'

18:47:17: 98304 bytes transferred in 0.016000 seconds (5.8594MBps)



18:47:17: File transferred successfully



18:47:17: Received file 'SHRM_MEM.BIN'

18:47:17: 65536 bytes transferred in 0.000000 seconds

18:47:17: File transferred successfully



18:47:17: Received file 'MSGRAM15.BIN'

18:47:17: 1024 bytes transferred in 0.015000 seconds (0.0651MBps)



18:47:17: File transferred successfully



18:47:17: Received file 'MSGRAM14.BIN'

18:47:17: 1024 bytes transferred in 0.000000 seconds

18:47:17: File transferred successfully



18:47:17: Received file 'MSGRAM13.BIN'

18:47:17: 1024 bytes transferred in 0.016000 seconds (0.0610MBps)



18:47:17: File transferred successfully



18:47:17: Received file 'MSGRAM12.BIN'

18:47:17: 1024 bytes transferred in 0.000000 seconds

18:47:17: File transferred successfully



18:47:17: Received file 'MSGRAM11.BIN'

18:47:17: 1024 bytes transferred in 0.000000 seconds

18:47:17: File transferred successfully



18:47:17: Received file 'MSGRAM10.BIN'

18:47:17: 1024 bytes transferred in 0.000000 seconds

18:47:17: File transferred successfully



18:47:17: Received file 'MSGRAM9.BIN'

18:47:17: 1024 bytes transferred in 0.000000 seconds

18:47:17: File transferred successfully



18:47:17: Received file 'MSGRAM8.BIN'

18:47:17: 1024 bytes transferred in 0.000000 seconds

18:47:17: File transferred successfully



18:47:17: Received file 'MSGRAM7.BIN'

18:47:17: 1024 bytes transferred in 0.000000 seconds

18:47:17: File transferred successfully



18:47:17: Received file 'MSGRAM6.BIN'

18:47:17: 1024 bytes transferred in 0.016000 seconds (0.0610MBps)



18:47:17: File transferred successfully



18:47:17: Received file 'MSGRAM5.BIN'

18:47:17: 1024 bytes transferred in 0.000000 seconds

18:47:17: File transferred successfully



18:47:17: Received file 'MSGRAM4.BIN'

18:47:17: 1024 bytes transferred in 0.000000 seconds

18:47:17: File transferred successfully



18:47:17: Received file 'MSGRAM3.BIN'

18:47:17: 1024 bytes transferred in 0.000000 seconds

18:47:17: File transferred successfully



18:47:17: Received file 'MSGRAM2.BIN'

18:47:17: 1024 bytes transferred in 0.000000 seconds

18:47:17: File transferred successfully



18:47:17: Received file 'MSGRAM1.BIN'

18:47:17: 1024 bytes transferred in 0.000000 seconds

18:47:17: File transferred successfully



18:47:17: Received file 'MSGRAM0.BIN'

18:47:17: 1024 bytes transferred in 0.000000 seconds

18:47:17: File transferred successfully



18:47:17: Received file 'DATARAM.BIN'

18:47:17: 32768 bytes transferred in 0.000000 seconds

18:47:17: File transferred successfully



18:47:17: Received file 'CODERAM.BIN'

18:47:17: 98304 bytes transferred in 0.016000 seconds (5.8594MBps)



18:47:17: File transferred successfully



18:47:17: Received file 'OCIMEM.BIN'

18:47:17: 262144 bytes transferred in 0.016000 seconds (15.6250MBps)



18:47:17: File transferred successfully



18:47:17: Successfully downloaded files from target

18:47:17: Sahara protocol completed

```
