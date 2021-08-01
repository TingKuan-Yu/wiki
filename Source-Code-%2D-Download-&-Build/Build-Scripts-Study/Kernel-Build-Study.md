# Building 8350 Kernel and Device Tree. For C1.
- https://dev.azure.com/E-OS/device/_wiki/wikis/Wiki/79354/Building-8350-Kernel-and-Device-Tree

## Default build creates a qgki-debug kernel
- default build method with fetch latest artifacts and dockers
  -fetch: fetch latest lib. Shall be using once a day

```
eos_build/scripts/kernel-build.sh -fetch
```
- default build method with fetch latest artifacts
  -nopull: not to pull docker
```
eos_build/scripts/kernel-build.sh -fetch -nopull
```
- specific kernel config by -c
  - if no -c, default is using "KERNCONFIG = lahaina-qgki-debug_defconfig".

# build log
   - [fetch_build.txt](/.attachments/fetch_build-86c3f63d-7835-47ee-91b7-bfb1aad58b29.txt)

# build flow
```
default build will call below command in docker:
build_command = device_build/kernel/kernel-build.sh -c lahaina-qgki-debug_defconfig -tb userdebug
--> finally it will call qualcomm script to build kernle
    ```
    echo "> Build Kernel HEADERS"
    HEADERS_INSTALL=1 device/qcom/kernelscripts/buildkernel.sh $TARGET_KERNEL_MAKE_ENV
    retval=$?
    if [ $retval -ne 0 ]; then
        echo "HEADERS failed $retval"
        return $retval &>/dev/null || exit $retval
    fi

    echo "> Build Kernel and modules"
    HEADERS_INSTALL=0 device/qcom/kernelscripts/buildkernel.sh $TARGET_KERNEL_MAKE_ENV
    retval=$?
    if [ $retval -ne 0 ]; then
        echo "BUILD failed $retval"
        return $retval &>/dev/null || exit $retval
    fi

    ```
```

