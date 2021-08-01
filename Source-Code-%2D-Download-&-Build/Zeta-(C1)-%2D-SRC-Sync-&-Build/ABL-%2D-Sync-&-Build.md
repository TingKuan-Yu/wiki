# reference
- https://dev.azure.com/E-OS/device/_wiki/wikis/Wiki/41457/Building-Locally-for-c1

# NHLOS

## RECOMMENDED: Sync all NHLOS
repo init -u ssh://ssh.dev.azure.com/v3/e-os/device/manifest -b c1/11/main -m nhlos/nhlos.xml

##Individual syncs if needed
repo init -u ssh://ssh.dev.azure.com/v3/e-os/device/manifest -b c1/11/main -m nhlos/abl.xml
repo init -u ssh://ssh.dev.azure.com/v3/e-os/device/manifest -b c1/11/main -m nhlos/adsp.xml
repo init -u ssh://ssh.dev.azure.com/v3/e-os/device/manifest -b c1/11/main -m nhlos/aop.xml
repo init -u ssh://ssh.dev.azure.com/v3/e-os/device/manifest -b c1/11/main -m nhlos/boot.xml
repo init -u ssh://ssh.dev.azure.com/v3/e-os/device/manifest -b c1/11/main -m nhlos/abl.xml
repo init -u ssh://ssh.dev.azure.com/v3/e-os/device/manifest -b c1/11/main -m nhlos/cdsp.xml
repo init -u ssh://ssh.dev.azure.com/v3/e-os/device/manifest -b c1/11/main -m nhlos/modem.xml
repo init -u ssh://ssh.dev.azure.com/v3/e-os/device/manifest -b c1/11/main -m nhlos/slpi.xml
repo init -u ssh://ssh.dev.azure.com/v3/e-os/device/manifest -b c1/11/main -m nhlos/tz.xml
repo init -u ssh://ssh.dev.azure.com/v3/e-os/device/manifest -b c1/11/main -m nhlos/meta.xml

## Sync the repo folder
repo sync -j 2

# Use Docker to build

build.sh will pull the container for you and run docker to do the individual builds. Use _debug for debug images. For example to build boot debug image, use ./build.sh build_boot_debug
./build.sh build_abl
./build.sh build_adsp
./build.sh build_aop
./build.sh build_boot (Note: ./build.sh build_boot_debug    for building DEBUG version of XBL)
./build.sh build_abl
./build.sh build_cdsp
./build.sh build_modem
./build.sh build_slpi
./build.sh build_tz
./build.sh build_meta
Get a Docker Build environment

# If you just want a docker shell that you can run commands in just like the build environment, run:
./build.sh -env 


# ABL
---
- Repo:
  - New: ADO -> device, priv-la.9.14-abl.tianocore.edk2
  - Old: ADO -> private-device, abl.tianocore.edk2

- Checkout
  - Under NHLOS:
    - repo init -u ssh://ssh.dev.azure.com/v3/e-os/device/manifest -b c1/11/main -m nhlos/abl.xml
    - repo sync –j 8
  - Under Vendor:
    - repo init -u ssh://ssh.dev.azure.com/v3/e-os/device/manifest -b c1/11/main -m vendor.xml
    - repo sync -c --no-tags --no-clone-bundle -j 8

- Build
  - Under NHLOS:
    - ./build.sh build_abl
    - can also build xbl: ./build.sh build_boot
  - Under Vendor:
    - eos_build/scripts/build.sh -env
    - source build/envsetup.sh && lunch oemc1-userdebug && make -j8 aboot

- Result
  - Bootable/bootloader/edk2/QcomModulePkg/Bin/RELEASE
    - abl.elf

- Clean
  - ./build.sh clean_abl
  - can also clean xbl: ./build.sh clean_boot

# XBL from NHLOS
---
- Repo:
  - New: ADO -> device, BOOT.MXF.1.0-premium-high-2020-spf-1-0_amss_standard_oem
  - Old: ADO -> device, qcom-BOOT.MXF.1.0-premium-high-2020-spf-1-0_amss_standard_oem

- Checkout
  - repo init -u ssh://ssh.dev.azure.com/v3/e-os/device/manifest -b c1/11/main -m nhlos/boot.xml
    - repo sync –j 8

- Build
 - ./build.sh build_boot

- Result
 - BOOT.MXF.1.0/boot_image/boot/QcomPkg/SocPkg/Lahaina/Bin/LAA/RELEASE/
 - xbl.elf, xbl_config.elf, and shrm.elf

- Clean
 - ./build.sh clean_boot

- Remove
 - rm -rf BOOT.MXF.1.0/boot_images/Build/
 - rm -rf BOOT.MXF.1.0/boot_images/boot/QcomPkg/SocPkg/Lahaina/Bin/LAA/RELEASE or DEBUG