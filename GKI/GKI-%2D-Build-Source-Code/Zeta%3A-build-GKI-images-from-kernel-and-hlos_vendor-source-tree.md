[[_TOC_]]

# Kernel GKI Build
---
## sync code
```
repo init -u ssh://ssh.dev.azure.com/v3/e-os/device/manifest -b c1/11/main -m kernel.xml
repo sync -c --no-tags --no-clone-bundle -j 2
```
## apply patches
  - https://dev.azure.com/E-OS/device/_git/caf-kernel.msm-5..4/commit/76cd1059ed7fc629df7cc8785c98f6f4d36e335e?refName=refs%2Fheads%2Fpersonal%2Ftony%2Fgki_enable_01
[0001-fix-disagrees-about-version-of-symbol-module_layout-.patch.tar.gz](/.attachments/0001-fix-disagrees- 
  - patch file: [0001-fix-disagrees-about-version-of-symbol-module_layout-.patch.tar.gz](/.attachments/0001-fix-disagrees-about-version-of-symbol-module_layout-.patch.tar-5401fccb-f044-4dde-aa2a-9ee2ad98144c.gz)

## Build with lahaina-gki_defconfig

- **Build Kernel tree**
  - first time with fetch
    ```
    eos_build/scripts/kernel-build.sh -c lahaina-gki_defconfig -tb user -fetch
    ```
  - not to fetch any more
    ```
    eos_build/scripts/kernel-build.sh -c lahaina-gki_defconfig -tb user
    ```
- Note: NOT to use below QGKI build
```
- QGKI
eos_build/scripts/kernel-build.sh -c lahaina-qgki_defconfig -tb user -fetch
- QGKI-DEBUG
eos_build/scripts/kernel-build.sh -c lahaina-qgki-debug_defconfig -tb userdebug -fetch
```

# hlos_vendor GKI Build
---
## copy kernel built objects hlos_vendor
```
mkdir -p vendor/surface/kernel
cd vendor/surface/kernel
cp ~/c1-11-kernel/getpkgs-install.sh .
cp ~/c1-11-kernel/*.zip .
```
## build vendor
- apply Amy's build patches in hlos_vendor/eos_build
  - [[0001-support-gki-build.patch.tar.gz](/.attachments/0001-support-gki-build.patch.tar-8b38bb8b-0dab-46df-b8d0-cbb3ee92c0cc.gz)]()

- build command    
```
eos_build/scripts/build.sh -l oemc1-user -sku default -c lahaina-gki_defconfig
```
