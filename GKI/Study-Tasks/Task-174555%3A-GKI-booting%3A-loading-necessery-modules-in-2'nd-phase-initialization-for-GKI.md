# patch
[0001-device-oemc1-load-wifi-modules-from-vendor_boot.patch.tar.gz](/.attachments/0001-device-oemc1-load-wifi-modules-from-vendor_boot.patch.tar-ef660830-b868-4d3b-9d34-43ff3308868c.gz)

# dump vendor_boot.img header
- https://source.android.com/devices/bootloader/partitions/vendor-boot-partitions
```
/*
Section	Number of pages
Vendor boot header (n pages)	n = (2108 + page_size - 1) / page_size
Vendor ramdisk (o pages)	o = (vendor_ramdisk_size + page_size - 1) / page_size
DTB (p pages)	p = (dtb_size + page_size - 1) / page_size
*/

/*
header ofvendor_boot.img

hexdump -C header

00000000  56 4e 44 52 42 4f 4f 54  03 00 00 00 00 10 00 00  |VNDRBOOT........|
00000010  00 80 00 00 00 00 00 01  d2 84 0a 00 63 6f 6e 73  |............cons|
00000020  6f 6c 65 3d 74 74 79 4d  53 4d 30 2c 31 31 35 32  |ole=ttyMSM0,1152|
00000030  30 30 6e 38 20 61 6e 64  72 6f 69 64 62 6f 6f 74  |00n8 androidboot|
00000040  2e 63 6f 6e 73 6f 6c 65  3d 74 74 79 4d 53 4d 30  |.console=ttyMSM0|
00000050  20 61 6e 64 72 6f 69 64  62 6f 6f 74 2e 6d 65 6d  | androidboot.mem|
00000060  63 67 3d 31 20 6c 70 6d  5f 6c 65 76 65 6c 73 2e  |cg=1 lpm_levels.|
00000070  73 6c 65 65 70 5f 64 69  73 61 62 6c 65 64 3d 31  |sleep_disabled=1|
00000080  20 76 69 64 65 6f 3d 76  66 62 3a 36 34 30 78 34  | video=vfb:640x4|
00000090  30 30 2c 62 70 70 3d 33  32 2c 6d 65 6d 73 69 7a  |00,bpp=32,memsiz|
000000a0  65 3d 33 30 37 32 30 30  30 20 6d 73 6d 5f 72 74  |e=3072000 msm_rt|
000000b0  62 2e 66 69 6c 74 65 72  3d 30 78 32 33 37 20 73  |b.filter=0x237 s|
000000c0  65 72 76 69 63 65 5f 6c  6f 63 61 74 6f 72 2e 65  |ervice_locator.e|
000000d0  6e 61 62 6c 65 3d 31 20  61 6e 64 72 6f 69 64 62  |nable=1 androidb|
000000e0  6f 6f 74 2e 75 73 62 63  6f 6e 74 72 6f 6c 6c 65  |oot.usbcontrolle|
000000f0  72 3d 61 36 30 30 30 30  30 2e 64 77 63 33 20 73  |r=a600000.dwc3 s|
00000100  77 69 6f 74 6c 62 3d 30  20 6c 6f 6f 70 2e 6d 61  |wiotlb=0 loop.ma|
00000110  78 5f 70 61 72 74 3d 37  20 63 67 72 6f 75 70 2e  |x_part=7 cgroup.|
00000120  6d 65 6d 6f 72 79 3d 6e  6f 6b 6d 65 6d 2c 6e 6f  |memory=nokmem,no|
00000130  73 6f 63 6b 65 74 20 70  63 69 65 5f 70 6f 72 74  |socket pcie_port|
00000140  73 3d 63 6f 6d 70 61 74  20 69 70 74 61 62 6c 65  |s=compat iptable|
00000150  5f 72 61 77 2e 72 61 77  5f 62 65 66 6f 72 65 5f  |_raw.raw_before_|
00000160  64 65 66 72 61 67 3d 31  20 69 70 36 74 61 62 6c  |defrag=1 ip6tabl|
00000170  65 5f 72 61 77 2e 72 61  77 5f 62 65 66 6f 72 65  |e_raw.raw_before|
00000180  5f 64 65 66 72 61 67 3d  31 20 61 6e 64 72 6f 69  |_defrag=1 androi|
00000190  64 62 6f 6f 74 2e 68 61  72 64 77 61 72 65 3d 6f  |dboot.hardware=o|
000001a0  65 6d 63 31 20 61 6e 64  72 6f 69 64 62 6f 6f 74  |emc1 androidboot|
000001b0  2e 68 61 72 64 77 61 72  65 2e 70 6c 61 74 66 6f  |.hardware.platfo|
000001c0  72 6d 3d 71 63 6f 6d 20  62 75 69 6c 64 76 61 72  |rm=qcom buildvar|
000001d0  69 61 6e 74 3d 75 73 65  72 00 00 00 00 00 00 00  |iant=user.......|
000001e0  00 00 00 00 00 00 00 00  00 00 00 00 00 00 00 00  |................|
*
00000810  00 00 00 00 00 00 00 00  00 00 00 00 00 01 00 00  |................|
00000820  00 00 00 00 00 00 00 00  00 00 00 00 00 00 00 00  |................|
00000830  40 08 00 00 65 35 39 00  00 00 f0 01 00 00 00 00  |@...e59.........|
00000840  00 00 00 00 00 00 00 00  00 00 00 00 00 00 00 00  |................|
*
00000ffb

#define VENDOR_RAMDISK_PAGES		(689362 + UFS_PAGE_SIZE -1 )/UFS_PAGE_SIZE

struct vendor_boot_img_hdr
{
#define VENDOR_BOOT_MAGIC_SIZE 8
    uint8_t magic[VENDOR_BOOT_MAGIC_SIZE]; /* Shall be VNDRBOOT */
    uint32_t header_version;      /* 03 00 00 00 */
    uint32_t page_size;           /* flash page size we assume */ /*00 10 00 00 --> 0x00001000 --> 4096*/

    uint32_t kernel_addr;         /* physical load addr */
    uint32_t ramdisk_addr;        /* physical load addr */ /*00 00 00 01 --> 0x01000000*/

    uint32_t vendor_ramdisk_size; /* size in bytes */ /*d2 84 0a 00 --> 0x000a84d2 -->  689362 bytes */

#define VENDOR_BOOT_ARGS_SIZE 2048
    uint8_t cmdline[VENDOR_BOOT_ARGS_SIZE];

    uint32_t tags_addr;           /* physical addr for kernel tags */

#define VENDOR_BOOT_NAME_SIZE 16
    uint8_t name[VENDOR_BOOT_NAME_SIZE]; /* asciiz product name */
    uint32_t header_size;         /* size of vendor boot image header in
                                   * bytes */
    uint32_t dtb_size;            /* size of dtb image */
    uint64_t dtb_addr;            /* physical load address */

};

*/
```
- Ubuntu Shell:
```
dd if=vendor_boot.img of=ramdisksize bs=1 skip=24 count=4
od -N4 -l ramdisksize | awk 'NR==1{ print $2}'  --> 689362
dd if=vendor_boot.img of=ramdisk.gz skip=1 bs=4096 count=169
gunzip -c ramdisk.gz > ramdisk
rm -rf extract && mkdir extract && pushd extract/ && cat ../ramdisk | cpio -idmv && popd
```
- Android sh:
```
LOCALDIR=${PWD}
rm -rf /data/local/vendor_boot
mkdir -p /data/local/vendor_boot
cd /data/local/vendor_boot
CURRENT_VENDOR_BOOT=$(ls /dev/block/by-name/vendor_boot* | grep `getprop ro.boot.slot_suffix`)                                                                                               
echo ${CURRENT_VENDOR_BOOT}
dd if=${CURRENT_VENDOR_BOOT} of=ramdisksize bs=1 skip=24 count=4
RAMDISK_SIZE=$(od -N4 -t u4 ramdisksize | awk 'NR==1{ print $2}')
echo ${RAMDISK_SIZE}
cala=`expr ${RAMDISK_SIZE} + 4095`
calb=`expr ${cala} / 4096`
#dd if=${CURRENT_VENDOR_BOOT} of=ramdisk.gz skip=4096 bs=1 count=${RAMDISK_SIZE}
dd if=${CURRENT_VENDOR_BOOT} of=ramdisk.gz skip=1 bs=4096 count=${calb}
gunzip ramdisk.gz
rm -rf extract ; mkdir extract ; cd extract/ ; cat ../ramdisk | cpio -idmv ;cd ..
```