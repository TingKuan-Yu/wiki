# source
- ./device_build/kernel/getpkgs-install.sh

# Function
## unzip kernel-headers.zip
- unzip to vendor/surface/kernel
- example log
```
> Process Kernel Headers
  - unzip /D/c1/11/main/hlos_vendor0608/vendor/surface/kernel/kernel-headers.zip
Archive:  /D/c1/11/main/hlos_vendor0608/vendor/surface/kernel/kernel-headers.zip
   creating: /D/c1/11/main/hlos_vendor0608/vendor/surface/kernel/kernel-headers/
  inflating: /D/c1/11/main/hlos_vendor0608/vendor/surface/kernel/kernel-headers/list.bp  
```

## unzip kernel-source.zip  
- unzip to hlos_vneodr/kernel
- example log
```
> Unzip Kernel Sources
  - unzip /D/c1/11/main/hlos_vendor0608/vendor/surface/kernel/kernel-source.zip
Archive:  /D/c1/11/main/hlos_vendor0608/vendor/surface/kernel/kernel-source.zip
  inflating: /D/c1/11/main/hlos_vendor0608/kernel/msm-5.4/net/dccp/output.c  
  inflating: /D/c1/11/main/hlos_vendor0608/kernel/msm-5.4/net/dccp/feat.h  
```

## unzip kernel.zip
- unzip to out
- example log
```
> Unzip Kernel Build
  - unzip /D/c1/11/main/hlos_vendor0608/vendor/surface/kernel/kernel.zip
Archive:  /D/c1/11/main/hlos_vendor0608/vendor/surface/kernel/kernel.zip
  inflating: /D/c1/11/main/hlos_vendor0608/out/target/product/oemc1/dlkm/lib/modules/qnoc-lahaina.ko  
  inflating: /D/c1/11/main/hlos_vendor0608/out/target/product/oemc1/dlkm/lib/modules/pinctrl_wcd_dlkm.ko  
:
 extracting: /D/c1/11/main/hlos_vendor0608/out/target/product/oemc1/dlkm/lib/modules/vendor_modules.zip  
:
 extracting: /D/c1/11/main/hlos_vendor0608/out/target/product/oemc1/dlkm/lib/modules/vendor_ramdisk_modules.zip  
:
 extracting: /D/c1/11/main/hlos_vendor0608/out/target/product/oemc1/obj/kernel/msm-5.4/net/802/modules.order 
```
