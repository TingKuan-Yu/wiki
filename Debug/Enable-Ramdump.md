[[_TOC_]]


# Reference
- ## Enable-Ram-Dumps-on-DV-Fused-devices
https://dev.azure.com/E-OS/Epsilon/_wiki/wikis/Epsilon.wiki/1352/Enable-Ram-Dumps-on-DV-Fused-devices-(Partial-or-Fully-Provisioned)

- ## Symbol file for ramdump
  - https://dev.azure.com/DSQO-Taipei/Knowledge%20Share/_wiki/wikis/Knowledge-Share.wiki/138/Symbol-file-for-ramdump

- ## c1-11-main-component is for symbol download
  - https://dev.azure.com/e-os/device/_packaging?_a=feed&feed=c1-11-main-component%40Local

# Ramdump Analysis Preparation
- ## download symbols
  - Make sure you build. It is better to know the exact version of the build. 
  - For example
    - **c1-11-selfhost-combo 2021.516.3**
  - Once you know the version, you can find out the web to download images.
    - https://dev.azure.com/E-OS/device/_packaging?_a=package&feed=c1-11-main-images&package=c1-11-selfhost-combo&protocolType=UPack&version=2021.516.3&view=overview
  - From the Description, you can get wiki for this image
    - https://dev.azure.com/E-OS/eos/_wiki/wikis/Integration-Builds?wikiVersion=GBmaster&pagePath=/Integration/c1-11-selfhost-c1-11-main-images/2021.516.3
  - From the Wiki **Builds** information, you can get the symbol files.
    - kernel symbol: https://dev.azure.com/E-OS/device/_packaging?_a=package&feed=c1-11-main-component&package=kernel-qgki&version=2021.512.7&protocolType=UPack
  - Then use Azure CLI to get symbol.
    - Get kernel symbol files
    ```    
    az artifacts universal download --organization "https://dev.azure.com/E-OS/" --feed "c1-11-main-component" --name "kernel-qgki" --version "2021.512.7" --path .
    ```
  - You may need to unzip files to get symbol images
    - unzip kernel.zip to get vmlinux
    ```
    unzip kernel.zip -d kernel
    ```
- ## install image with perf test script
  - ./flash_test_perf.sh
    - **cause Symbol Mismatch**

- ## Make sure the rawdump partiton is empty
  - 1. at fastboot mode
    - fastboot erase rawdump
  - 2. at adb mode
    -  make sure the rawdump partition is empty
    ```
    adb root
    adb shell cat /dev/block/by-name/rawdump
    ```

# Test Ramdump
- ## check ram dump mode
  - adb root; adb shell
  ```
  c1:/ # cat /sys/kernel/dload/dload_mode                                                                                                                                                                           
  DLOAD dump type: mini
  c1:/ # cat /sys/kernel/dload/emmc_dload                                                                                                                                                                           
  1
  ```
  - **to get ramdump by QPST or QSaharaServer, you need to** 
    ``` echo 0 > /sys/kernel/dload/emmc_dload  ```
- ## make force a ramdump
  ```
  c1:/ # echo c > /proc/sysrq-trigger 
  ```

# Use QUD Linux to get ramdump
- get radmump
  - reference: https://dev.azure.com/tingkuanyu/TingKuanYuPrivate1/_wiki/wikis/TingKuanYuPrivate1.wiki/220/QUD-Get-Ramdump
```
sudo ./fh_loader/QSaharaServer.bin -p "/dev/QTI_HS-USB_Diagnostics_900E_1-10.1:1.0" -m -w ./tmp/
```
- copy vmlinux to above tmp folder 

# run QCAP for analysis
- run qcap
  - Location and APPS path
    - /D/c1/11/images/selfhost-combo/2021.516.3/ramdump/tmp
  - Press "Full Analysis" button
- kernel symbol
```
strings ~/dump/DDRCS0_0.BIN | grep "^Linux version 5.4" | head -n 1 | awk '{print  $3}' | tail -c 11|sed 's/_/\./g'

strings vmlinux | grep "Linux version"

uname -a

```

# Note: fix missing libssl1.0.0 in ubuntu20.4 
```
Edit the source list sudo nano /etc/apt/sources.list to add the following line: deb http://security.ubuntu.com/ubuntu xenial-security main
Then sudo apt update and sudo apt install libssl1.0.0.
```



