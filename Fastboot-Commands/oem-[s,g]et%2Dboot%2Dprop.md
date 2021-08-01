# Reference
---
- https://dev.azure.com/E-OS/device/_wiki/wikis/Wiki/227063/Setting-the-oem-keys
  - fastboot oem set-boot-prop product.hardware.sku gen
  ```
  DEFVAR: CHECK: product.hardware.sku
  [_CmdOemGetBootProp] - 
  product.hardware.sku=gen
  DEFVAR: GOT:   product.hardware.sku=gen
  Adding to commandline - androidboot.product.hardware.sku=gen
  ```

# Test 
---
## add boot property
- fastboot command
```
tingkuanyu@TonyYuLinux1:/D/c1/11/main/abl$ fastboot oem set-boot-prop key1 tony
(bootloader) 
CmdOemSetBootPropCore: Success

OKAY [  0.009s]
Finished. Total time: 0.009s
tingkuanyu@TonyYuLinux1:/D/c1/11/main/abl$ fastboot oem get-boot-prop key1
(bootloader) 
key1=tony
(bootloader) 

OKAY [  0.002s]
Finished. Total time: 0.002s
tingkuanyu@TonyYuLinux1:/D/c1/11/main/abl$ fastboot reboot
```
- adb command 
```
tingkuanyu@TonyYuLinux1:/D/c1/11/main/abl$ adb shell getprop | grep key1
[ro.boot.key1]: [tony]
[ro.oem.key1]: [tony]
```

## delete boot property
- fastboot command
```
tingkuanyu@TonyYuLinux1:/D/c1/11/main/abl$ fastboot oem del-boot-prop key1
(bootloader) 
CmdOemSetBootPropCore: Success

OKAY [  0.009s]
Finished. Total time: 0.009s
tingkuanyu@TonyYuLinux1:/D/c1/11/main/abl$ fastboot oem get-boot-prop key1
FAILED (remote: 'Not found or enough resources
')
fastboot: error: Command failed
tingkuanyu@TonyYuLinux1:/D/c1/11/main/abl$ fastboot reboot

```
- adb command
```
tingkuanyu@TonyYuLinux1:/D/c1/11/main/abl$ adb shell getprop | grep key1
```