# Link
- https://dev.azure.com/E-OS/Zeta/_workitems/edit/156614

# Analysis
```
According to ABL booting flow, there are some conditions:
1. If device is not Unbootable (means bootable), booting to OS
2. If device is not Unbootable, not BootSuccess and the RetryCount is greater than 0
   1) new flash device if retry count 6
   2) really unbootable and retry if retry count < 6
3. unbootable
   The log will show "Slot %s is unbootable, trying alternate slot". %s is either a or b
   
According to the log from Oscar, I think that he flashed a new version, booting to OS and then reboot again.

Form the respective of UEFI, the system is bootable because there is no retry count which is smaller than 6.
There is no Slot %s is unbootable, trying alternate slot", either.

The system shall boot to Android and then rebooting again.
If there are logcat logs which recorded at the issue time, it could be easier to find out the root cause.


Since there is no "Run  Cycle :" log on user build, I only guess the log starts from UefuLog1.txt.

UefiLog1.txt:

POST Time      [ 2740] OS Loader
Loader Build Info: May  5 2021 01:21:09
Fastboot=0, Recovery:0
Booting from slot (_b)

UefiLog2.txt: new OS, first boot
POST Time      [ 2739] OS Loader
Loader Build Info: May 10 2021 23:26:34
Fastboot=0, Recovery:0
Active Slot _a is bootable, retry count 6
Booting from slot (_a)

UefiLog3.txt: no retry count, so slot is bootable
POST Time      [ 2010] OS Loader
Loader Build Info: May 10 2021 23:26:34
Fastboot=0, Recovery:0
Booting from slot (_a)
Booting Into Mission Mode

UefiLog4.txt:  no retry count, so slot is bootable
POST Time      [ 1985] OS Loader
Loader Build Info: May 10 2021 23:26:34
Fastboot=0, Recovery:0
Booting from slot (_a)
Booting Into Mission Mode

```