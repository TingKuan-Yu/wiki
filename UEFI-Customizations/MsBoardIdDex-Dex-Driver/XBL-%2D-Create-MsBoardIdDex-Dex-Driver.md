# Fundamental steps
## 1. create MsBoardIdDex in BOOT.MXF.1.0/boot_images/boot/Sm8350FamilyPkg/Drivers

## 2. create MsBoardIdDex.inf for build this module
- reference
  - https://edk2-docs.gitbook.io/edk-ii-module-writer-s-guide/8_dxe_drivers_non-uefi_drivers/81_beginning_with_inf_file
  - https://edk2-docs.gitbook.io/edk-ii-module-writer-s-guide/8_dxe_drivers_non-uefi_drivers/82_write_dxe_driver_entry_point
  - http://manpages.ubuntu.com/manpages/bionic/man1/uuidgen.1.html
  - generate uuid with uuidgen tool


## 3. create MsBoardIdDexMain.c for main driver function
- PROTOCOL REVISION study
  - https://edk2-docs.gitbook.io/edk-ii-uefi-driver-writer-s-guide/22_text_console_driver_design_guidelines/readme.4#example-230-simple-text-output-protocol
 

# BOOT.MXF.1.0/boot_images/boot/Sm8350FamilyPkg/Drivers/MsBoardIdDex.inf

# fdf


# ABL Patch
- https://dev.azure.com/E-OS/device/_git/caf-abl.tianocore.edk2/commit/e06b5b3e6e3887762cb744f52201b3e2fb71a775?refName=refs%2Fheads%2Fperson%2Ftony%2Fuefi%2Fprj_id
  - person/tony/uefi/prj_id

# XBL Patch 
- https://dev.azure.com/E-OS/device/_git/qcom-BOOT.MXF.1.0-premium-high-2020-spf-1-0_amss_standard_oem/commit/53fc64e9148b40c7969a44e4e5017787c0ff2012?refName=refs%2Fheads%2Fperson%2Ftony%2Fuefi%2Fprj_id
  - person/tony/uefi/prj_id


```
tingkuanyu@TonyYuLinux1:/D/c1/11/main/abl_prj_id/bootable/bootloader/edk2$ fastboot oem get-board-id
(bootloader) Project ID:: 0x1

OKAY [  0.001s]
Finished. Total time: 0.001s

c1:/ $ getprop ro.boot.brdprjid                                                                                                                                                                              
1

```