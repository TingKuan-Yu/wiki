
- search
```
avc: denied { search } for comm="ls" name="block" dev="tmpfs" ino=14499 scontext=u:r:vendor_modprobe:s0 tcontext=u:object_r:block_device:s0 tclass=dir permissive=0
```

- execute_no_trans
```
avc: denied { execute_no_trans } for path="/vendor/bin/awk" dev="dm-3" ino=82 scontext=u:r:vendor_modprobe:s0 tcontext=u:object_r:vendor_file:s0 tclass=file permissive=0
```

- getattr
```
avc: denied { getattr } for comm="ls" path="/dev/block/sde21" dev="tmpfs" ino=10717 scontext=u:r:vendor_modprobe:s0 tcontext=u:object_r:boot_block_device:s0 tclass=blk_file permissive=0
```

- module_load
```
avc: denied { module_load } for comm="modprobe" path="/data/vendor/modprobe/vendor_boot/lib/modules/cnss_utils.ko" dev="dm-5" ino=8135 scontext=u:r:vendor_modprobe:s0 tcontext=u:object_r:vendor_modprobe_file:s0 tclass=system permissive=0

```

- neverallow on line 1308 of system/sepolicy/public/domain.te
```
FAILED: out/target/product/oemc1/obj/ETC/sepolicy.recovery_intermediates/sepolicy
/bin/bash -c "(ASAN_OPTIONS=detect_leaks=0 out/host/linux-x86/bin/checkpolicy -M -c 		30 -o out/target/product/oemc1/obj/ETC/sepolicy.recovery_intermediates/sepolicy.tmp out/target/product/oemc1/obj/ETC/sepolicy.recovery_intermediates/sepolicy.recovery.conf ) && (out/host/linux-x86/bin/sepolicy-analyze out/target/product/oemc1/obj/ETC/sepolicy.recovery_intermediates/sepolicy.tmp permissive > out/target/product/oemc1/obj/ETC/sepolicy.recovery_intermediates/sepolicy.permissivedomains ) && (if [ \"user\" = \"user\" -a -s out/target/product/oemc1/obj/ETC/sepolicy.recovery_intermediates/sepolicy.permissivedomains ]; then 		echo \"==========\" 1>&2; 		echo \"ERROR: permissive domains not allowed in user builds\" 1>&2; 		echo \"List of invalid domains:\" 1>&2; 		cat out/target/product/oemc1/obj/ETC/sepolicy.recovery_intermediates/sepolicy.permissivedomains 1>&2; 		exit 1; 		fi ) && (mv out/target/product/oemc1/obj/ETC/sepolicy.recovery_intermediates/sepolicy.tmp out/target/product/oemc1/obj/ETC/sepolicy.recovery_intermediates/sepolicy )"
libsepol.report_failure: neverallow on line 1308 of system/sepolicy/public/domain.te (or line 13390 of policy.conf) violated by allow vendor_modprobe vendor_modprobe_file:system { module_load };
libsepol.check_assertions: 1 neverallow failures occurred
Error while expanding polic
```


---
```
[3:08 PM] Tony Yu
out/target/product/oemc1/vendor/etc/selinux/vendor_file_contexts: line 630 has invalid context u:object_r:vendor_file_type:s0

[3:09 PM] Tony Yu
/data/vendor/modprobe/vendor_boot(/.*)?                 u:object_r:vendor_file_type:s0

[3:10 PM] Tony Yu
定義data下的file type出錯.

[3:11 PM] Tony Yu
原本為 allow vendor_modprobe vendor_modprobe_file:system module_load;

[3:11 PM] Tony Yu
# Enforce restrictions on kernel module origin.
# Do not allow kernel module loading except from system,
# vendor, and boot partitions.
neverallow * ~{ system_file_type vendor_file_type rootfs }:system


```