# Android_boot_image_editor
- https://github.com/cfig/Android_boot_image_editor


# Unpack boot.img
- cd Android SRC root
```
mkdir unpack_test
cp out/target/product/oemc1/boot.img unpack_test/
cp ./out/soong/host/linux-x86/bin/unpack_bootimg unpack_test/
cp out/host/linux-x86/lib64/ unpack_test/ -af



```