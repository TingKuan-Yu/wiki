# Reference
- https://dev.azure.com/E-OS/device/_wiki/wikis/Wiki/34172/Building-C1-Zeta-on-Android-11?anchor=vendor-build


# Vendor Sync (mirror recommended)
```
mkdir ~/11/c1
pushd ~/11/c1
repo init -u ssh://ssh.dev.azure.com/v3/e-os/device/manifest -b c1/11/main -m hlos.xml
repo sync -c --no-tags --no-clone-bundle -j 2
```
# Vendor Build
- 1. Make sure we export AZURE_DEVOPS_EXT_PAT with your own PAT
- 2. Make sure you read this: Building-8350-Kernel-and-Device-Tree
  - https://dev.azure.com/E-OS/device/_wiki/wikis/Wiki?wikiVersion=GBmaster&pagePath=%2FDeveloper%20Guide%2FWelcome%20to%20Android%2011%2FBuilding%208350%20Kernel%20and%20Device%20Tree
  - copy sh and zip file to vendor source
  ```
  mkdir -p vendor/surface/kernel
  cd vendor/surface/kernel
  cp ~/c1-11-kernel/getpkgs-install.sh .
  cp ~/c1-11-kernel/*.zip .
  ```
- 3. You can build vendor now
  - You can remove **-fetch** if you have done it once after syncing
  ```
  eos_build/scripts/build.sh -fetch -l oemc1-userdebug -sku default
  ```

# Vendor Flash
- NOTE: the .img files are located at out/target/product/oemc1
```
adb reboot fastboot
fastboot flash vendor vendor.img
```


