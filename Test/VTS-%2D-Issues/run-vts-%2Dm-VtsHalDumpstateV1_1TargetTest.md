# 2021.516.3
- scontext=u:r:hal_dumpstate_impl:s0 tcontext=u:object_r:property_socket:s0 tclass=sock_file 
```
01-29 13:16:11.236   956   956 W libc    : Unable to set property "persist.vendor.verbose_logging_enabled" to "true": connection failed; errno=13 (Permission denied)
01-29 13:16:11.234   956   956 I auditd  : type=1400 audit(0.0:219): avc: denied { write } for comm="dumpstate@1.1-s" name="property_service" dev="tmpfs" ino=12936 scontext=u:r:hal_dumpstate_impl:s0 tcontext=u:object_r:property_socket:s0 tclass=sock_file permissive=0
01-29 13:16:11.234   956   956 W dumpstate@1.1-s: type=1400 audit(0.0:219): avc: denied { write } for name="property_service" dev="tmpfs" ino=12936 scontext=u:r:hal_dumpstate_impl:s0 tcontext=u:object_r:property_socket:s0 tclass=sock_file permissive=0

```
# Local build test 1
- set persist.vendor.verbose_logging_enabled as default
- scontext=u:r:hal_dumpstate_impl:s0 tcontext=u:object_r:vendor_default_prop:s0 tclass=property_service 
```
01-29 13:16:22.200     1     1 I auditd  : type=1107 audit(0.0:910): uid=0 auid=4294967295 ses=4294967295 subj=u:r:init:s0 msg='avc: denied { set } for property=persist.vendor.verbose_logging_enabled pid=953 uid=1000 gid=1000 scontext=u:r:hal_dumpstate_impl:s0 tcontext=u:object_r:vendor_default_prop:s0 tclass=property_service permissive=1'
01-29 13:16:22.200     1     1 I /system/bin/init: type=1107 audit(0.0:910): uid=0 auid=4294967295 ses=4294967295 subj=u:r:init:s0 msg='avc: denied { set } for property=persist.vendor.verbose_logging_enabled pid=953 uid=1000 gid=1000 scontext=u:r:hal_dumpstate_impl:s0 tcontext=u:object_r:vendor_default_prop:s0 tclass=property_service permissive=1'

```

# Local build test 2
- set allow in te file
  - allow hal_dumpstate_impl vendor_default_prop:property_service { set };
```
neverallow check failed at out/target/product/oemc1/obj/ETC/plat_pub_versioned.cil_intermediates/plat_pub_versioned.cil:5458
  (neverallow base_typeattr_223_30_0 vendor_default_prop_30_0 (property_service (set)))
    <root>
    allow at out/target/product/oemc1/obj/ETC/vendor_sepolicy.cil_intermediates/vendor_sepolicy.cil:2937
      (allow hal_dumpstate_impl vendor_default_prop_30_0 (property_service (set)))

neverallow check failed at out/target/product/oemc1/obj/ETC/plat_sepolicy.cil_intermediates/plat_sepolicy.cil:7351 from system/sepolicy/public/domain.te:530
  (neverallow base_typeattr_226 vendor_default_prop (property_service (set)))
    <root>
    allow at out/target/product/oemc1/obj/ETC/vendor_sepolicy.cil_intermediates/vendor_sepolicy.cil:2937
      (allow hal_dumpstate_impl vendor_default_prop_30_0 (property_service (set)))
```

# Local build test 3
Sepolicy Issue. This issue can't be fixed. It shall be an issue of the VTS test tool. 

01-29 13:16:11.236   956   956 W libc    : Unable to set property 

- domain.te
```
# Only the init property service should write to /data/property and /dev/__properties__
neverallow { domain -init } property_type:file { no_w_file_perms no_x_file_perms };
```












