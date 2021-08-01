# Task
- https://dev.azure.com/E-OS/Zeta/_sprints/taskboard/UEFI/Zeta/Software%20Iteration/Backlog/2021/Sprint%2011%20(5-16-2021%20-%205-28-2021)?workitem=159402


# Create a new adbkey on your host
- from https://gist.github.com/pantasio/3d0eb4bb03a1e696aae8696f60730859#file-enable-usb-debug-adb
```
rm -v .android/adbkey* .android/adbkey .android/adbkey.pub 
adb keygen .android/adbkey 
```
# Enable adb for selfhost/gen image
- 1. flash device with test_perf script
   - ./flash_test_perf.sh

- 2. enable develop mode
```
adb shell settings put global development_settings_enabled 1
```
- 3. enable adb
  - from https://stackoverflow.com/questions/32132434/set-adb-vendor-keys
```
adb root
adb shell setprop persist.service.adb.enable 1                                                    
adb shell setprop persist.service.debuggable 1
adb shell setprop persist.sys.usb.config mtp,adb
```
Note: 
  1. step 2 & 3 could be replaced by _fastboot oem set-adb-kernel-param_ for our build
  2. disable setup wizard - https://gist.github.com/nemanjan00/a3c39d94b41f0cc4c4b7e7f404f3fd8a 
  ```
  settings put global setup_wizard_has_run 1
  settings put secure user_setup_complete 1
  settings put global device_provisioned 1
  ```

- 4. copy from PC .android/adbkey.pub (pubkic key) to Device on path /data/misc/adb/adb_keys
```
adb root
adb push ~/.android/adbkey.pub /data/misc/adb/adb_keys
adb shell "chmod 776 /data/misc/adb/adb_keys"
```

- 5. reboot bootloader to flash user build boot and vendor_boot image
```
adb reboot bootloader
fastboot flash boot boot.img
fastboot flash vendor_boot vendor_boot.img
fastboot reboot
```

- 6. now you shall be able to use adb without authorization. 
