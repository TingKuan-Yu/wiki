# reference
## SM8350 Software Debug Manual (SP80-PK177-5)

## QCT document -  Linux Android UEFI Integration ( 80-P2484-37 K )
- 7.5.1 Load UEFI ramdump and analyze
Use the load_uefi_dump.cmm to load the dump and analyse using Trace32.
To use the load_uefi_dump.cmm, set up the paths using the scripts in the following steps:
  - Run the command in T32 to set the UEFI core path:
  ```
  cd.do bootable/bootloader/edk2/QcomModulePkg/Tools/uefi_core_path_set.cmm <path to uefi xbl core >
  ```
  - Run the command to set the abl path:
  ```
  cd.do bootable/bootloader/edk2/QcomModulePkg/Tools/app_path_set.cmm  <AppObjPath> <AppSrcPath>
  ```
  - Run the command to load the dump:
  ```
  cd.do load_uefi_dump.cmm <path to dump>
  ```

# Make UEFI crash
## Set address 0 to a value
```
  EFI_STATUS Status = EFI_SUCCESS; UINT32 *Foo = 0;
  *Foo = 1;
```



================================
To collect and debug crashdumps, use the following procedure: 1. Collect crashdumps using the "QPST Configuration" tool when the device is in Sahara crashdump mode.
This is typically indicated by the display showing "Crashdump Mode".
Dumps are automatically collected to the following location:
C:\ProgramData\Qualcomm\QPST\Sahara\Port_COMXX 2. Launch T32 Simulator APPS window and run the load_uefi_dump.cmm script which takes the rampdump
directory as an argument. For example:
cd.do load_uefi_dump.cmm C:\ProgramData\Qualcomm\QPST\Sahara\Port_COM10
after above loads the ramdump and symbols, use the following to switch the CPU's fast
cd.do load_uefi_dump.cmm NOLOAD <CPU NUM> The rampdump and symbols will be loaded and debugging related windows (source code, call stack, registers,
etc.) will be displayed.
NOTE: It is recommended to use the load_uefi_dump.cmm script from the "ABL" QcomModulePkg/Tools directory
for debugging ramdumps collected due to crash in ABL

[Monday 3:17 PM] Tony Yu
依文件, 取出的ramdump可用T32 Simulator APPS window來debug

[Monday 3:19 PM] Tony Yu
To enable UEFI ramdump, add ENABLE_RAMDUMP, as added in red in the example
DSC file.  但找code似乎沒看到.

[Monday 3:20 PM] Tony Yu
Ramdump is not collected in the
release binary. After a crash, the ramdump will be collected using the QPST tool.

[Monday 3:22 PM] Tony Yu
Load the ramdump using the load_uefi_dump.cmm script.Once the ramdump is loaded, the stack and the code that caused the crash will beproduced. Add similar code wherever a crash must be analyzed.

