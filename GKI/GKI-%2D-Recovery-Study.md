# Recovery module loading
- In prior Android releases, kernel modules required for recovery were specified in BOARD_RECOVERY_KERNEL_MODULES. In Android 11, kernel modules required for recovery are still specified using this macro. However, the recovery kernel modules are copied to the vendor ramdisk cpio, rather than the generic ramdisk cpio. By default all kernel modules listed in BOARD_RECOVERY_KERNEL_MODULES are loaded during first-stage init. If you only want a subset of these modules to be loaded, specify the contents of that subset in BOARD_RECOVERY_KERNEL_MODULES_LOAD.
  - Currently, the ko files listed in kernel.json decides which module be placed in vendor_boot if the module is set m in kernel config. It also decides the content of modules.load.  If the ko files you need are placed in the vendor-ramdisk/lib/modules and the modules.load file lists their names without BOARD_RECOVERY_KERNEL_MODULES setting, I think you can remove BOARD_RECOVERY_KERNEL_MODULES . If you set BOARD_RECOVERY_KERNEL_MODULES_LOAD, the recovery process will use modules.load.recovery instead of modules.load. If you have no special loading sequence for recovery to load modules, you needn't to use BOARD_RECOVERY_KERNEL_MODULES_LOAD, either. 

- reference
  - https://source.android.com/devices/architecture/kernel/kernel-module-support

- note set BOARD_RECOVERY_KERNEL_MODULES_LOAD --> modules.load.recovery
- first_stage_init.cpp
```
std::string GetModuleLoadList(bool recovery, const std::string& dir_path) {
    auto module_load_file = "modules.load";
    if (recovery) {
        struct stat fileStat;
        std::string recovery_load_path = dir_path + "/modules.load.recovery";
        if (!stat(recovery_load_path.c_str(), &fileStat)) {
            module_load_file = "modules.load.recovery";
        }
    }

    return module_load_file;
}


```

# fastbootd
- /system/bin/fastbootd in ramdisk not in system.img
- https://source.android.com/devices/bootloader/fastbootd


# related task
- https://dev.azure.com/E-OS/Zeta/_workitems/edit/177861
- https://dev.azure.com/E-OS/device/_git/device.oemc1.oemc1/pullrequest/23603

# VTS skip fastbootd
- https://android-review.googlesource.com/c/platform/test/vts/+/1495577
- https://android-review.googlesource.com/c/platform/test/vts/+/1495577/1/testcases/host/fastboot_test/src/com/android/tests/FastbootVerifyUserspaceTest.java
- https://android.googlesource.com/platform/test/vts/+/3f3e47a883abdfccd1760acb3eac9211d6f5f3b6