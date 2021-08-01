# C1 11 Multi-PR web
- https://dev.azure.com/E-OS/device/_build?definitionId=1614
  - Select Run pipeline
  - Select gki multipr branch
  - fill in your PRs
  - Press Run
![Multi-PR.png](/.attachments/Multi-PR-7aa9c790-6dee-47c1-9868-4e8a5f65d73b.png)
- Bootable Artifacts
  - https://dev.azure.com/E-OS/device/_build/results?buildId=710068&view=results
    - Bootable with adb but no display.

# Flash GKI Multi-PR
1. flash slefhost combo with  test perf script
2. adb reboot fastboot
3. flash image download from Multi-PR under fastbootd mode then reboot too bootloader
```
fastboot flash vendor vendor.img 
fastboot flash odm odm.img
reboot to bootloader
```
4. flash images at bootloader mode
```
fastboot flash boot boot.img
fastboot flash vendor_boot vendor_boot-debug.img
fastboot flash dtbo dtbo.img 
fastboot --disable-verity flash vbmeta vbmeta.img
fastboot -w 
fastboot reboot
```