Share my study of SM8350 Boot about CoreBSP Architecture Overview doc and xbl source.

For cold boot described in doc.
4a-4c.

XBL_Loader initializes hardware and firmware images, CPU caches, MMU, boot devices, XBLConfig, PMIC, DDR, SHRM, and SMEM (shared memory). XBL_Loader fills platform ID and RAM partition table, performs DDR training if applicable, and executes an SCM call to XBL_SEC to initialize Pseudo IMEM (pIMEM). XBL_Loader also initializes and configures the clock frequencies as per the clock plan;
loads and authenticates the APPS debug policy (APDP) image from the boot device.

XBL_Loader loads and authenticates eXtensible boot loader (XBL) RAM dump, if the DLOAD cookie is set, and jumps to XBL RAM dump to collect the crash dump.
--> Shall be no DLOAD cookie for cold boot. Please refer to the warm reset flow for DLOAD cookie.
 
:
4k. XBL_Loader loads and authenticates XBL core image from the boot device.
1) boot_images/boot/QcomPkg/XBLCore/Sec.c
   Main (IN  VOID  *StackBase, IN  UINTN StackSize) ->  UefiBootContinue() -> InitDbiDump() -> SetDLOADCookie()
   Note: uefiplat.cfg
     # for full dump 0x10, for minidump 0x20
     DloadCookieValue = 0x10
  
     --> Before setting ram dump mode to mini by the kernel, it shall be full dump once crash occurred between XBL core and msm-poweroff kernel module.

    Change DloadCookieValue to 0x20 may help.

Since each reboot is cold boot for normal reboot, the imem would be clean and the imem for cookie would be also clean. So, Bert's patch is necessary.
https://dev.azure.com/e-os/device/_git/qcom-BOOT.MXF.1.0-premium-high-2020-spf-1-0_amss_standard_oem/commit/58f23526c486ed43652cc25ef406a8ad6dd2a804?refName=refs%2Fheads%2Fpersonal%2Fbert%2Fsigned_image_xbl
- boot_ram_initc
```
if (boot_shared_imem_cookie_ptr->shared_imem_magic !=
        BOOT_SHARED_IMEM_MAGIC_NUM)
:
   boot_shared_imem_cookie_ptr->uefi_ram_dump_magic =
        BOOT_RAW_RAM_DUMP_MAGIC_NUM;

```

Note: crash cause warm reset.

Test:
add below code in abl 
CmdShowHWDevInfo ()
  int *i = 0;
  int j = 1;
   *i=j; // force ramdum

      2. flash new abl 
      3. reboot bootloader
      4. use "fastboot oem show-hw-devinfo" to trigger panic.

Test log:
fullrawdump_putty.log  
Bert's XBL patch only: https://dev.azure.com/e-os/device/_git/qcom-BOOT.MXF.1.0-premium-high-2020-spf-1-0_amss_standard_oem/commit/58f23526c486ed43652cc25ef406a8ad6dd2a804?refName=refs%2Fheads%2Fpersonal%2Fbert%2Fsigned_image_xbl

Handling Cmd: oem show-hw-devinfo
unhandled synchronous exception
ESR 0xF2000001: ec 0x3C, il 0x2000000, iss 0x1
iframe 0x9f429e20:
:
B -    937753 - TCSR reg value 0x10
:
B -   1440271 - Raw Partition Dump
B -   1441338 - RawDump: Dump start address:0x14680000, size 0x40000
B -   1450915 - RawDump: Dump start address:0xb000000, size 0x18000
B -   1460279 - RawDump: Dump start address:0xb0e0000, size 0x8000
B -   1468087 - RawDump: Dump start address:0xc300000, size 0x400
B -   1474888 - RawDump: Dump start address:0xc310000, size 0x400
minirawdump-putty.log
Bert's XBL patch https://dev.azure.com/e-os/device/_git/qcom-BOOT.MXF.1.0-premium-high-2020-spf-1-0_amss_standard_oem/commit/58f23526c486ed43652cc25ef406a8ad6dd2a804?refName=refs%2Fheads%2Fpersonal%2Fbert%2Fsigned_image_xbl
PLUS 
 uefiplat.cfg
     # for full dump 0x10, for minidump 0x20
     DloadCookieValue = 0x20


Handling Cmd: getvar:version
Handling Cmd: oem show-hw-devinfo
unhandled synchronous exception
ESR 0xF2000001: ec 0x3C, il 0x2000000, iss 0x1
:
B -   1173396 - TCSR reg value 0x20
:
B -   1676097 - Raw Partition Dump
B -   1678323 - RawDump: Dump start address:0x1f6c28000, size 0x6e60
B -   1686802 - RawDump: Dump start address:0x1112000, size 0x6000
B -   1694519 - RawDump: Dump start address:0x1f7139080, size 0xd80
B -   1701747 - RawDump: Dump start address:0xa28607e0, size 0x10
B -   1708762 - RawDump: Dump start address:0xe3807e50, size 0x800
B -   1715991 - RawDump: Dump start address:0xe3808690, size 0x800
