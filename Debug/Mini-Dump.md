[[_TOC_]]


# Tasks
- XBL minidump encryption key
  - https://dev.azure.com/E-OS/Zeta/_workitems/edit/110766/

# Wiki
- https://dev.azure.com/E-OS/Zeta/_wiki/wikis/Zeta.wiki/146018/Mini-Ram-Dumps
  - Presently decompressing and parsing mini dumps are only supported for mini dumps from unfused devices

- [Mini Ram Dumps - Overview (azure.com)](https://nam06.safhttps://nam06.safelinks.protection.outlook.com/?url=https%3A%2F%2Fdev.azure.com%2FE-OS%2FZeta%2F_wiki%2Fwikis%2FZeta.wiki%2F137044%2FParse-Ram-dump-with-Power-shell-script&data=04%7C01%7Ctony.yu%40microsoft.com%7Cbc30206960ba4610520608d91e892f8c%7C72f988bf86f141af91ab2d7cd011db47%7C1%7C0%7C637574396830040304%7CUnknown%7CTWFpbGZsb3d8eyJWIjoiMC4wLjAwMDAiLCJQIjoiV2luMzIiLCJBTiI6Ik1haWwiLCJXVCI6Mn0%3D%7C1000&sdata=wNSUcHXKJl7VEx8KOVxXUM2rXRkGnNPMKM%2FknL%2BFgRU%3D&reserved=0elinks.protection.outlook.com/?url=https%3A%2F%2Fdev.azure.com%2FE-OS%2FZeta%2F_wiki%2Fwikis%2FZeta.wiki%2F146018%2FMini-Ram-Dumps&data=04%7C01%7Ctony.yu%40microsoft.com%7Cbc30206960ba4610520608d91e892f8c%7C72f988bf86f141af91ab2d7cd011db47%7C1%7C0%7C637574396830030306%7CUnknown%7CTWFpbGZsb3d8eyJWIjoiMC4wLjAwMDAiLCJQIjoiV2luMzIiLCJBTiI6Ik1haWwiLCJXVCI6Mn0%3D%7C1000&sdata=Zzi1CL%2FRk3HVkW9vJEyzZd7b1eGcIBsvqFnBwoLj6Ww%3D&reserved=0)
- [Collecting & Parsing Ram Dumps - Overview (azure.com)](https://nam06.safelinks.protection.outlook.com/?url=https%3A%2F%2Fdev.azure.com%2FE-OS%2FZeta%2F_wiki%2Fwikis%2FZeta.wiki%2F58488%2FCollecting-Parsing-Ram-Dumps&data=04%7C01%7Ctony.yu%40microsoft.com%7Cbc30206960ba4610520608d91e892f8c%7C72f988bf86f141af91ab2d7cd011db47%7C1%7C0%7C637574396830030306%7CUnknown%7CTWFpbGZsb3d8eyJWIjoiMC4wLjAwMDAiLCJQIjoiV2luMzIiLCJBTiI6Ik1haWwiLCJXVCI6Mn0%3D%7C1000&sdata=WBV3vW%2BDI%2BAqax0ppRupMB9m9OHv4ndaOtxkYYoslYg%3D&reserved=0)
- [Parse Ram dump with Power shell script - Overview (azure.com)](https://nam06.safelinks.protection.outlook.com/?url=https%3A%2F%2Fdev.azure.com%2FE-OS%2FZeta%2F_wiki%2Fwikis%2FZeta.wiki%2F137044%2FParse-Ram-dump-with-Power-shell-script&data=04%7C01%7Ctony.yu%40microsoft.com%7Cbc30206960ba4610520608d91e892f8c%7C72f988bf86f141af91ab2d7cd011db47%7C1%7C0%7C637574396830040304%7CUnknown%7CTWFpbGZsb3d8eyJWIjoiMC4wLjAwMDAiLCJQIjoiV2luMzIiLCJBTiI6Ik1haWwiLCJXVCI6Mn0%3D%7C1000&sdata=wNSUcHXKJl7VEx8KOVxXUM2rXRkGnNPMKM%2FknL%2BFgRU%3D&reserved=0)
- [Downloading Symbols for Ram dump Analysis - Overview (azure.com)](https://nam06.safelinks.protection.outlook.com/?url=https%3A%2F%2Fdev.azure.com%2FE-OS%2FZeta%2F_wiki%2Fwikis%2FZeta.wiki%2F135362%2FDownloading-Symbols-for-Ram-dump-Analysis&data=04%7C01%7Ctony.yu%40microsoft.com%7Cbc30206960ba4610520608d91e892f8c%7C72f988bf86f141af91ab2d7cd011db47%7C1%7C0%7C637574396830050293%7CUnknown%7CTWFpbGZsb3d8eyJWIjoiMC4wLjAwMDAiLCJQIjoiV2luMzIiLCJBTiI6Ik1haWwiLCJXVCI6Mn0%3D%7C1000&sdata=nK3qMO2513g7B5ydvywB%2F9ZXde%2FjpZN03SIR6i3aG1Y%3D&reserved=0)


# Steps
## 1. prepare tools
  - Copy the tools from \\desmo\wds\Devices\Zeta\Users\kgoel\minidump-tools

## 2. check kernel version
```
c1:/ $ uname -a
Linux localhost 5.4.61-c1-p-2021_512_7 #1 SMP PREEMPT Thu May 13 06:23:11 UTC 2021 aarch64
c1:/ $ getprop ro.bootimage.build.fingerprint
sf/c1-gen/c1:11/2021.513.6/202105130006:user/release-keys
```

## 3. download kernel symbo
- From step 2, the kernel version is **5.4.61-c1-p-2021_512_7** and it is a **user** build.
- Download from **kernel-qgki** for user build. Select **2021.512.7**.
  - https://dev.azure.com/E-OS/device/_packaging?_a=package&feed=c1-11-main-component&package=kernel-qgki&protocolType=UPack&version=2021.512.7&view=overview
```
C:\zeta\minidump\kernel-qgki\2021.512.7>az artifacts universal download --organization "https://dev.azure.com/E-OS/" --feed "c1-11-main-component" --name "kernel-qgki" --version "2021.512.7" --path .
{
  "Description": "$(publish)",
  "ManifestId": "36642287E16B54982AAD368A5E35D515872DF40BA614AD9E72DA1387986DD00E01",
  "SuperRootId": "0848ADC2618483F8C4D669AC7A18BC6AE0E590357FACC0F870BF8B852D4D764C02",
  "Version": "2021.512.7"
}
```

## 4. check mindump folder.
If there is a folder, delete it.
```
adb root
adb shell ls /data/vendor/ramdump/
```

## 5. make sure minidump setting
```
1|c1:/ # cat /sys/kernel/dload/dload_mode
DLOAD dump type: mini
c1:/ # cat /sys/kernel/dload/emmc_dload
1
```

## 6. trigger a ramdump
```
c1:/ # echo c > /proc/sysrq-trigger
```
- I can also see md gz file in /data/vendor/ramdump folder with below condition.
  - **flash_selfhost + non-fused device + mfg mode + long press power key to 13s**
  - pon power key is set to software reset

## 7. Pull mindump image
- After ramdump rebooting to OS, use below command to get dump.
```
adb root
adb pull /data/vendor/ramdump/minidump
```

## 8. unzip the gz file that pulled from the device. Then, use a tool such as 7Zip to unzip it.

## 9. check every tool and image are ready
- tools: Copy the tools from \\desmo\wds\Devices\Zeta\Users\kgoel\minidump-tools
- vmlinux: use corresponding version
```
05/24/2021  04:34 PM    <DIR>          decrpt_out
02/09/2021  05:57 PM             4,080 generate_appself.py
05/24/2021  04:30 PM       208,240,640 md_1970-0-1-21s
02/22/2021  01:12 PM            68,884 minidump_decrypt_decompress_tool.py
05/13/2021  02:31 PM       533,537,040 vmlinux
```

## 10. run the scripts
```
C:\Python27\python.exe minidump_decrypt_decompress_tool.py -s md_1970-0-1-21s decrpt_out
C:\Python27\python.exe generate_appself.py decrpt_out
copy vmlinux .\decrpt_out
```

## 11. Use QCAP to parsing ramdump
- Chipset: LAHAINA
- Software Product: LAHAINA.LA.1.0.C8
- Log location and APPS all select the decrpt_out fold
  - Example
    - C:\zeta\minidump\minidump\custom-gen\decrpt_out

## 12. Source code
- vendor
  - vendor/surface/crashdump/mdCollectord.rc
- kernel
  - kernel/msm-5.4/drivers/power/reset/msm-poweroff.c
- hal
  - zip /dev/block/by-name/rawdump to /data/vendor/ramdump/minidump/minidump_%d-%d-%d_%d-%d-%d_%s.gz
    - https://dev.azure.com/E-OS/ssi/_git/platform.vendor.surface.integrationservice?path=%2Fintegration_hal%2Fproviders%2Fcrash_dump.cpp
