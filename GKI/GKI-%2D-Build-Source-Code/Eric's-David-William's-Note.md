# build
```
[6/9/2021 2:25 PM] Eric Lee (SURFACE)
I did my local build as follwoing.download the GKI artificats and copy the zip files to into my vendor build. (/vendor/surface/kernel)
	unzip the GKI module to out folder (bash gepkgs-install.sh)
	eos_build/scripts/build.sh -env
	export KERNEL_DEFCONFIG=gki_defconfig && export BUILD_NUMBER=1.2.3 && source build/envsetup.sh && lunch oemc1-user
	make vendorbootimage 

[6/9/2021 2:25 PM] Eric Lee (SURFACE)
my change for the venderboot can be found in this branch.https://dev.azure.com/e-os/device/_git/device.oemc1.oemc1

[6/9/2021 2:26 PM] Eric Lee (SURFACE)
feel free to push ur change to my branch

```

[6/8/2021 11:07 AM] Eric Lee (SURFACE)
https://dev.azure.com/e-os/device/_packaging?_a=package&feed=c1-11-main-component&package=kernel-gki&protocolType=UPack&version=2021.607.1



[6/8/2021 11:09 AM] Eric Lee (SURFACE)
https://dev.azure.com/e-os/device/_build/results?buildId=686405&view=results



[6/8/2021 11:11 AM] Eric Lee (SURFACE)
https://dev.azure.com/e-os/device/_build/results?buildId=686405&view=logs&j=dccf73ab-cb1c-5558-611d-aa0037d9bf27&t=e4499ca8-72f9-5fe3-7153-fb9fbbd3f1ef



[6/8/2021 11:11 AM] Eric Lee (SURFACE)
https://dev.azure.com/e-os/device/_build/results?buildId=686405&view=logs&j=dccf73ab-cb1c-5558-611d-aa0037d9bf27&t=e4499ca8-72f9-5fe3-7153-fb9fbbd3f1ef&l=30



[6/8/2021 11:33 AM] Tony Yu
~/qct_src/hi2020-c8_00007.7/out/target/product/lahaina/vendor/lib/modules/5.4-gki$

[6/8/2021 11:36 AM] Tony Yu
tingkuanyu@TonyYuLinux1:~/qct_src/hi2020-c8_00007.7/out/target/product/lahaina/obj$ ls -al | grep -i kernel
drwxrwxr-x 3 tingkuanyu tingkuanyu 4096 Jun 1 19:25 kernel
drwxrwxr-x 3 tingkuanyu tingkuanyu 4096 Jun 1 19:25 kernel-gki
lrwxrwxrwx 1 tingkuanyu tingkuanyu 14 Jun 1 20:39 KERNEL_OBJ -> kernel/msm-5.4

[6/8/2021 11:38 AM] Eric Lee (SURFACE)
https://dev.azure.com/e-os/device/_packaging?_a=package&feed=c1-11-main-component&package=kernel-gki&version=2021.607.1&protocolType=UPack



[6/8/2021 11:38 AM] Eric Lee (SURFACE)
az artifacts universal download --organization "https://dev.azure.com/E-OS/" --feed "c1-11-main-component" --name "kernel-qgki" --version "2021.607.1" --path .



[6/8/2021 11:38 AM] Eric Lee (SURFACE)
https://dev.azure.com/e-os/device/_packaging?_a=package&feed=c1-11-main-component&package=kernel-qgki&protocolType=UPack&version=2021.607.1



