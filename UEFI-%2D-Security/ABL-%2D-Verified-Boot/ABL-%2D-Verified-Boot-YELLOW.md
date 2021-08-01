# Locked devices with a custom key set
- https://source.android.com/security/verifiedboot/boot-flow#locked-devices-with-custom-key-set

# Steps for custom key
- **Overview**
  - One way of implementing user-settable root of trust is to have a virtual partition that can only be flashed or cleared when the device is in the UNLOCKED state. The Google Pixel 2 devices use this approach and the virtual partition is called avb_custom_key. 
- **Generate custom key**
  - The format of the data in this partition is the output of the avbtool extract_public_key command. Here's an example of how to set the user-settable root of trust:
  ```
  avbtool extract_public_key --key key.pem --output pkmd.bin
  ```
- Flash or erase key
```
fastboot flash avb_custom_key pkmd.bin
fastboot erase avb_custom_key
```

# Test on Zeta
 

Go back to fastboot.
Run: fastboot flash vbmeta <attached vbmeta>.
Run: fastboot fastboot flash avb_custom_key <attached key>
Run: fastboot flashing lock

# Library/avb/KeymasterClient.c