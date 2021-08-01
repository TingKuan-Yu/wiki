
-repack vendor_boot.img
```
tools/mkbootimg/mkbootimg.py --header_version 3 --dtb /mnt/data3/android-kernel/lahaina-v2.1.dtb --vendor_ramdisk /mnt/data3/android-kernel/vendor_ramdisk --pagesize 0x00001000 --base 0x00000000 --kernel_offset 0x00008000 --ramdisk_offset 0x01000000 --tags_offset 0x00000100 --dtb_offset 0x00190000 --vendor_cmdline 'console=ttyMSM0,115200n8 androidboot.console=ttyMSM0 androidboot.memcg=1 lpm_levels.sleep_disabled=1 video=vfb:640x400,bpp=32,memsize=3072000 msm_rtb.filter=0x237 service_locator.enable=1 androidboot.usbcontroller=a600000.dwc3 swiotlb=0 loop.max_part=7 cgroup.memory=nokmem,nosocket pcie_ports=compat iptable_raw.raw_before_defrag=1 ip6table_raw.raw_before_defrag=1 androidboot.hardware=oemc1 androidboot.hardware.platform=qcom androidboot.mode=userdebug buildvariant=userdebug' --board ''   --vendor_boot /mnt/data3/android-kernel/out/android11-5.4/dist/vendor_boot.img
```
- tools/mkbootimg/mkbootimg.py 
  -  --header_version 3
  -  --dtb /mnt/data3/android-kernel/lahaina-v2.1.dtb
  -  --vendor_ramdisk /mnt/data3/android-kernel/vendor_ramdisk
  -  --pagesize 0x00001000
  -  --dtb_offset 0x00190000 
  -  --vendor_cmdline 'console=ttyMSM0,115200n8 androidboot.console=ttyMSM0 androidboot.memcg=1 lpm_levels.sleep_disabled=1 video=vfb:640x400,bpp=32,memsize=3072000 msm_rtb.filter=0x237 service_locator.enable=1 androidboot.usbcontroller=a600000.dwc3 swiotlb=0 loop.max_part=7 cgroup.memory=nokmem,nosocket pcie_ports=compat iptable_raw.raw_before_defrag=1 ip6table_raw.raw_before_defrag=1 androidboot.hardware=oemc1 androidboot.hardware.platform=qcom androidboot.mode=userdebug buildvariant=userdebug'
  -  --board ''
  - --vendor_boot /mnt/data3/android-kernel/out/android11-5.4/dist/vendor_boot.img 