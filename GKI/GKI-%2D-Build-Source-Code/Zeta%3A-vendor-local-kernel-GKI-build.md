
# GKI Local Test Build

## Enable uart on GKI for test build
- lahaina_GKI.config
  - CONFIG_MSM_GENI_SE=m
    - CONFIG_MSM_GENI_SE=y
  - CONFIG_SERIAL_MSM_GENI=m
    - CONFIG_SERIAL_MSM_GENI=y
  - \+ SERIAL_MSM_GENI_HALF_SAMPLING=y
  - \+ SERIAL_MSM_GENI_EARLY_CONSOLE=y
  - \+ CONFIG_SERIAL_MSM_GENI_CONSOLE=y
- Note: system init.rc
```
on init && property:ro.debuggable=1
    start console
```

## Note for lahaina_QGKI.config
- \#CONFIG_DEBUG_FS=y 
  - shall be set to \#CONFIG_DEBUG_FS is not set

## build configuration
- device/oemc1/oemc1/BoardConfig.mk
```
+ # TingKuanYu
+ SURFACE_BUILD_KERNEL := 1
```
- remove all if SURFACE_BUILD_KERNEL definition
  - device/kernelscripts/kernel_definitions.mk

- eos/scripts/kernel-build.sh
  - from KERNCONFIG=$(cat device_build/build.json | jq -r .defaults.kernConfig)
    - to KERNCONFIG=lahaina-qgki_defconfig
    - force user build

## Build
- build kernel
```
eos_build/scripts/kernel-build.sh -c lahaina-gki_defconfig -tb user -fetch
```
- fetch and copy
```
eos_build/scripts/build.sh -fetchonly
tingkuanyu@TonyYuLinux1:/D/c1/11/main/hlos_vendor0531$ cp ../kernel/vendor/qcom/proprietary/devicetree/ vendor/qcom/proprietary/ -af
tingkuanyu@TonyYuLinux1:/D/c1/11/main/hlos_vendor0531$ cp ../kernel/vendor/qcom/proprietary/display-devicetree/ vendor/qcom/proprietary/ -af
tingkuanyu@TonyYuLinux1:/D/c1/11/main/hlos_vendor0531$ cp ../kernel/vendor/qcom/proprietary/camera-devicetree/ vendor/qcom/proprietary/ -af
```

- change ramdump mode to full
  - msm-poweroff.c
    - static int msm_restart_probe(struct platform_device *pdev)
    ```
    - dload_type = SCM_DLOAD_MINIDUMP;
    + dload_type = SCM_DLOAD_FULLDUMP;
    ```
- skip MSCHANGE in setlocalversion of kernel
- cp files from hi2020 kernel
  - because we don't use vendor/surface/kernel as header
```
cp ~/qct_src/hi2020/kernel/msm-5.4/Android.bp kernel/msm-5.4/
cp ~/qct_src/hi2020/kernel/msm-5.4/gen_headers_arm*.bp kernel/msm-5.4/
cp /home/tingkuanyu/qct_src/hi2020/kernel/msm-5.4/kernel_headers.py kernel/msm-5.4/kernel_headers.py
```


- build
  - setup and lunch
  ```
  eos_build/scripts/build.sh -env
  source build/envsetup.sh
  lunch oemc1-user
  ```
  - select vendor/lahaina-**q**gki_defconfig
    - reason
    ```
    ifeq "$(KERNEL_DEFCONFIG)" "vendor/$(TARGET_BOARD_PLATFORM)-qgki_defconfig"
    BOARD_KERNEL_BINARIES := kernel kernel-gki
    ```
    - build command
    ```
    ./build.sh -j8 KERNEL_DEFCONFIG=vendor/lahaina-qgki_defconfig --target_only -j16
    ```



# flash gki build
- 1. flash slefhost combo
  - test perf script
- 2. adb reboot fastboot
- 3. fastboot flash vendor and odm
  ```
  fastboot flash vendor vendor.img 
  fastboot flash odm odm.img
  ```
- 4. reboot to bootloader
- 5. fastboot flash boot-gki-debug.img and vendor_boot-debug.img
```
fastboot flash boot boot-debug-gki.img
fastboot flash vendor_boot vendor_boot-debug.img
fastboot flash dtbo dtbo.img 
fastboot --disable-verity flash vbmeta vbmeta.img
```
- 6 . fastboot -w and fastboot reboot

# booting error
- disagrees about version of symbol module_layout
```
rmnet_ctl: disagrees about version of symbol module_layout
```

