# Reference Doc
- Build GKI with console enabled
  - KBA-201222232647
- Android Generic Kernel Image
  - 80-13043-3

# Sync code
```
mkdir common-android11-5.4
cd common-android11-5.4/
repo init -u https://android.googlesource.com/kernel/manifest -b common-android11-5.4
repo sync
```
# Check gki version
- check release note
- 00007.7 Release Note for Snapdragon_Premium_High_2020.SPF.1.0.c8
  - Building GKI kernel: (For debug purpose only)
   - 1. Instructions for syncing and compilation are available at
        https://source.android.com/setup/build/building-kernels
   - 2. Lahaina uses common-android11-5.4 branch.
   - 3. Recommend to reset kernel tree to the following commit to be in line with this Lahaina release.
      "4271ad6e8ade BACKPORT: mac80211_hwsim: add frame transmission support over virtio This allows        communication with external entities.

# Reset to gki version
```
cd common 
git reset --hard 4271ad6e8ade
or git checkout 4271ad6e8ade
```

# Compile Google GKI
```
KBUILD_SYMTYPES=1 BUILD_CONFIG=common/build.config.gki.aarch64 build/build.sh
```

# build boot-gki.img
- use common-android11-5.4/tools/mkbootimg/unpack_bootimg.py to unpack/pack gki image
```
tingkuanyu@TonyYuLinux1:/E/GKI/common-android11-5.4$ mkdir pack_boot

tingkuanyu@TonyYuLinux1:/E/GKI/common-android11-5.4$ cp /E/xTS/gsi/signed-aosp_arm64-img-7111047/boot-5.4-gz.img pack_boot/

tingkuanyu@TonyYuLinux1:/E/GKI/common-android11-5.4$ tools/mkbootimg/unpack_bootimg.py --boot_img=pack_boot/boot-5.4-gz.img
boot magic: ANDROID!
kernel_size: 13437263
ramdisk size: 8261946
os version: 11.0.0
os patch level: 2021-02
boot image header version: 3
command line args: buildvariant=user

tingkuanyu@TonyYuLinux1:/E/GKI/common-android11-5.4$ mv out/ramdisk pack_boot/gki-ramdisk.lz4
```
- repeat build once ramdisk is ready
```
tingkuanyu@TonyYuLinux1:/E/GKI/common-android11-5.4$ BUILD_BOOT_IMG=1 SKIP_VENDOR_BOOT=1 
KERNEL_BINARY=Image.gz GKI_RAMDISK_PREBUILT_BINARY=pack_boot/gki-ramdisk.lz4 BUILD_CONFIG=common/build.config.gki.aarch64 build/build.sh

``` 

# Patch to skip module magic version check
- vermagic
```
tingkuanyu@TonyYuLinux1:/D/c1/11/main/hlos_vendor0531/out/target/product/oemc1$ modinfo ./vendor-ramdisk/lib/modules/5.4-gki/proxy-consumer.ko
filename:       /D/c1/11/main/hlos_vendor0531/out/target/product/oemc1/./vendor-ramdisk/lib/modules/5.4-gki/proxy-consumer.ko
description:    Regulator proxy consumer library
license:        GPL v2
vermagic:       5.4.61 SMP preempt mod_unload modversions aarch64
name:           proxy_consumer
intree:         Y
depends

tingkuanyu@TonyYuLinux1:~/qct_src/hi2020-c8_00007.7/out/target/product/lahaina$ modinfo ./vendor-ramdisk/lib/modules/5.4-gki/proxy-consumer.ko
filename:       /home/tingkuanyu/qct_src/hi2020-c8_00007.7/out/target/product/lahaina/./vendor-ramdisk/lib/modules/5.4-gki/proxy-consumer.ko
description:    Regulator proxy consumer library
license:        GPL v2
vermagic:       5.4.61-00002-g6513445841c4-dirty SMP preempt mod_unload modversions aarch64
name:           proxy_consumer
intree:         Y
depends:

```