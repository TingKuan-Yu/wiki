[[_TOC_]]


# PR 13318: Adding support for max CPUs in cmdline
- oem set-maxcpu-kernel-param
- oem clear-maxcpu-kernel-param"

# PR 13408: Change the partition type for userdata from ext4 to f2fs in ABL fastboot
```
-    {"userdata", "partition-size:", "partition-type:", "", "ext4"},
+    {"userdata", "partition-size:", "partition-type:", "", "f2fs"}, //MS_CHANGE
```

# PR 13808: Add Selfhost and Production AVB keys to ABL
- OEMProductionPublicKey & OEMSelfhostPublicKey
```
+// MSCHANGE Support Production and Selfhost keys
+// TODO as part of 50675: enable #ifdef SHIP_MODE to only allow OEMProductionPublicKey in SHIP_MODE
+	} else if (PublicKeyLength == ARRAY_SIZE(OEMProductionPublicKey) &&
+	           CompareMem(PublicKeyData, OEMProductionPublicKey, PublicKeyLength) == 0) {
+		*OutIsTrusted = true;
+	} else if (PublicKeyLength == ARRAY_SIZE(OEMSelfhostPublicKey) &&
+	           CompareMem(PublicKeyData, OEMSelfhostPublicKey, PublicKeyLength) == 0) {
+		*OutIsTrusted = true;
```

# PR 14069: Enabling battery fastboot cmds
- enabled shipmode: fastboot.exe oem battery-shipmode
- enabled battery rsoc query from fastboot: fastboot.exe getvar battery-level

# PR 14345: Add a sfpd protocol caller in ABL
- There is no method to access FAT32 partition in ABL now.
- This patch add a sfpd access protocol in XBL so that ABL can use the library of XBL to access SFPD.

# PR 14373: Manufacturing Mode Porting on ABL
- Add Manufacturing Mode Live and Ms Fastboot Cmds libraries
- Implement a new protocol between XBL and ABL to check the current mode and flash variable services
- Add fastboot oem commands for manufacturing mode
- Increase ABL Image Size
- Related work items: #50616


# PR 14934: Move ABL to NHLOS Build
- Implement buildconfig.json in QcomModulePkg to compile ABL and create abl.elf image
- Modify BuildEnv in BaseTools to try edk2 root first for setting EDK_TOOLS_PATH
- Modify QcomModulePkg.dsc to add CC flags
- Change the name ABL_OUT_DIR to ABLOUTDIR for fixing replace argument problem (no under line) in makefile
- Related work items: #84651
- ## PR 15124: Move ABL to NHLOS Build
  - Related work items: #84651, #90693