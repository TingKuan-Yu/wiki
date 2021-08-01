
```
cp out/target/product/oemc1/obj/PACKAGING/vendor-boot_intermediates/vendor-ramdisk.cpio.gz tony/
cd tony
gunzip vendor-ramdisk.cpio.gz 
cat vendor-ramdisk.cpio | cpio -idmv
```