# build/make/target/product/base_system.mk
```
# Packages included only for eng or userdebug builds, previously debug tagged
PRODUCT_PACKAGES_DEBUG := \
    adb_keys \

```

# build/make/target/product/security/Android.mk
- PRODUCT_ADB_KEYS
```
# adb key, if configured via PRODUCT_ADB_KEYS
ifdef PRODUCT_ADB_KEYS
  ifneq ($(filter eng userdebug,$(TARGET_BUILD_VARIANT)),)
    include $(CLEAR_VARS)
    LOCAL_MODULE := adb_keys
    LOCAL_MODULE_CLASS := ETC
    LOCAL_MODULE_PATH := $(TARGET_ROOT_OUT)
    LOCAL_PREBUILT_MODULE_FILE := $(PRODUCT_ADB_KEYS)
    include $(BUILD_PREBUILT)
  endif
endif

```
# bootable/recovery/README.md
- ADB_VENDOR_KEYS
```
 * **Option 1 (Recommended):** Authorize a host device with adb vendor keys.

For debuggable builds, an RSA keypair can be used to authorize a host device that has the private
key. The public key, defined via `PRODUCT_ADB_KEYS`, will be copied to `/adb_keys`. When starting
the host-side `adbd`, make sure the filename (or the directory) of the matching private key has been
added to `$ADB_VENDOR_KEYS`.

    $ export ADB_VENDOR_KEYS=/path/to/adb/private/key
    $ adb kill-server
    $ adb devices

`-user` builds filter out `PRODUCT_ADB_KEYS`, so no `/adb_keys` will be included there.

Note that this mechanism applies to both of normal boot and recovery modes.


```