# AOSP Links
- ramdisk-partitions
  - Topic about init file
  - https://source.android.com/devices/bootloader/partitions/ramdisk-partitions
  - The init in ramdisk comes from init_first_stage.
    ```
    system/core/init/Android.mk:
      LOCAL_MODULE := init_first_stage
      LOCAL_MODULE_STEM := init
    ```

