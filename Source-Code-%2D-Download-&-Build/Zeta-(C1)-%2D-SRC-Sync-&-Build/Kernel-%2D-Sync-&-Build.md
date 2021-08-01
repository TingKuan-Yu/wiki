
# from
- https://dev.azure.com/E-OS/device/_wiki/wikis/Wiki/79354/Building-8350-Kernel-and-Device-Tree

For 8350, the kernel and device tree build has been moved to a stand-alone build that generates artifacts consumed by the vendor build.  This enables faster local and PR builds for kernel work plus helps meet our open-source obligations for publishing code.

# Build Kernel and Device Tree
## Sync
```
repo init -u ssh://ssh.dev.azure.com/v3/e-os/device/manifest -b c1/11/main -m kernel.xml
repo sync -c --no-tags --no-clone-bundle -j 2
```
## Build 
```
#Default build creates a qgki-debug kernel
eos_build/scripts/kernel-build.sh -fetch
```
### Kernel Flavors
#### GKI
```
eos_build/scripts/kernel-build.sh -c lahaina-gki_defconfig -tb user -fetch
```

#### QGKI
```
eos_build/scripts/kernel-build.sh -c lahaina-qgki_defconfig -tb user -fetch
```

#### QGKI-DEBUG
```
eos_build/scripts/kernel-build.sh -c lahaina-qgki-debug_defconfig -tb userdebug -fetch
```

#### MTEOS
```
$eos_build/scripts/kernel-build.sh -fetch --sku mteos
```

## Output
The following artifacts are produced from the build at the top of the enlistment
### kernel-headers.zip
Zip file containing all of the processed user space kernel headers
### kernel-source.zip
Zip of the kernel source used for the build.  Required for Vendor build in the OS since Qualcomm builds vendor modules outside this kernel build
### kernel.zip
Zip of the object files, binaries and symbols for the kernel and device tree

# Integrate into local Vendor Build
- Create a standard local vendor build
- Copy kernel.zip, kernel-source.zip and kernel-headers.zip to vendor/surface/kernel and overwrite the existing files
```
cd ~/11/c1
mkdir -p vendor/surface/kernel
cd vendor/surface/kernel
cp ~/c1-11-kernel/getpkgs-install.sh .
cp ~/c1-11-kernel/*.zip .
```
- Process the new .zip files
```
bash getpkgs-install.sh
```
- Rebuild your local vendor build to generate a new boot.img and dtbo.img

# Build Infrastructure
## Artifacts
Kernel Artifacts (listed below) are pulled into the vendor build here:
https://dev.azure.com/E-OS/device/_git/artifacts.vendor?path=%2Fpackages-vendor.json&version=GBc1%2F11%2Fmain&_a=contents
## Kernel Build Pipeline
https://dev.azure.com/E-OS/device/_build?definitionId=1910&_a=summary
## Kernel Source
https://dev.azure.com/E-OS/device/_git/priv-la.9.14-kernel.msm-5..4?path=%2F&version=GBc1%2F11%2Fmain&_a=contents
## Kernel Build Artifacts
### GKI
https://dev.azure.com/E-OS/device/_packaging?_a=package&feed=c1-11-main-component&package=kernel-gki&version=2020.1114.2&protocolType=UPack
### QGKI
https://dev.azure.com/E-OS/device/_packaging?_a=package&feed=c1-11-main-component&package=kernel-qgki&version=2020.1114.2&protocolType=UPack
### QGKI-DEBUG
https://dev.azure.com/E-OS/device/_packaging?_a=package&feed=c1-11-main-component&package=kernel-qgki-debug&version=2020.1114.2&protocolType=UPack