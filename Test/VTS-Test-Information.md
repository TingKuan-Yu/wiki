
# Google's Requirement
![xts.png](/.attachments/xts-b210778b-0770-4dbf-9432-b7b072eb7cb2.png)

# download GSI and VTS tool from xts lab
- https://dev.azure.com/e-os/device/_packaging?_a=feed&feed=xts-lab-tpe%40Local

# VTS installation
- 1. unlock mfg mode
- 2. fastboot flashing unlock
- 3. fastboot flashing unlock-critical
- 4. fastboot oem clear-mfg-mode
- 5. change flashmap.testperf.json
  - "args": ["vbmeta.img","--disable-verity"] --> "args": ["vbmeta.img"]
  - "args": ["boot-debug.img"] --> "args": ["boot.img"]
- 6. flash image
  - ./flash_selfhost.sh
- 7. after rebooting to Android. Execute "adb reboot fastboot" to flash gsi.
- 8. after rebooting to fastbootd. 
  - fastboot flash system system.img
    - not system.img is gsi image
  - fastbppt erase userdata
  - fastboot reboot
- 9. Now the system shall be at GSI Android desktop now.

# try a test
```
run vts -m vts_security_avb_test --test AvbTest#SystemDescriptor
```