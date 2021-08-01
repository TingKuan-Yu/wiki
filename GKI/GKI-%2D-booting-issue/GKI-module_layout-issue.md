# Reporting maodule_layout error when insmod to GKI kernel
```
rmnet_ctl: disagrees about version of symbol module_layout
```

# Check issue
- search module_layout abi_gki_aarch64
  - include/linux/module.h
  - kernel/module.c
```
abi_gki_aarch64.xml:2648: <elf-symbol name='module_layout' type='func-type' binding='global-binding' visibility='default-visibility' is-defined='yes' crc='0x1e5b7ab7'/>
abi_gki_aarch64.xml:5406: <class-decl name='module_layout' size-in-bits='640' is-struct='yes' visibility='default' filepath='include/linux/module.h' line='309' column='1' id='68b3d9a8'>
abi_gki_aarch64.xml:44065: <class-decl name='module_layout' size-in-bits='640' is-struct='yes' visibility='default' filepath='include/linux/module.h' line='309' column='1' id='68b3d9a8'>
abi_gki_aarch64.xml:149380: <function-decl name='module_layout' mangled-name='module_layout' filepath='kernel/module.c' line='4614' column='1' visibility='default' binding='global' size-in-bits='64' elf-symbol-id='module_layout'>
Found 6 matches for "module_layout".
```

# compare c1 kernel to hi2020 for all these files 
  - kernel/msm-5.4/arch/arm64/kernel/module.c
    - changed by ftrace