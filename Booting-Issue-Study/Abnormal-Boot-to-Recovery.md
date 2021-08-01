# Related Tasks or Bugs
- User Device Was Running Warm, Said Something Abnormal Occurred and Hit Recovery
  - https://dev.azure.com/E-OS/Zeta/_workitems/edit/156614

# vold/cryptfs.cpp
- int cryptfs_enable_internal(int crypt_type, const char* passwd, int no_ui)
  - cryptfs_reboot(RebootType::recovery);
```
        property_get("ro.vold.wipe_on_crypt_fail", value, "0");
        if (!strcmp(value, "1")) {
            /* wipe data if encryption failed */
            SLOGE("encryption failed - rebooting into recovery to wipe data\n");
            std::string err;
            const std::vector<std::string> options = {
                "--wipe_data\n--reason=cryptfs_enable_internal\n"};
            if (!write_bootloader_message(options, &err)) {
                SLOGE("could not write bootloader message: %s", err.c_str());
            }
            cryptfs_reboot(RebootType::recovery);
        } else {
            /* set property to trigger dialog */
            property_set("vold.encrypt_progress", "error_partially_encrypted");
        }
```