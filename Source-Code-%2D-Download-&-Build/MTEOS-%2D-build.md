
vendor

https://dev.azure.com/E-OS/device/_git/manifest?path=%2Fyaml%2Fvendor-build.yaml&version=GBc1%2F11%2Fmain&_a=contents

eos_build/scripts/build.sh -fetch -l oemc1-userdebug -sku mteos

merge:

https://dev.azure.com/E-OS/device/_git/manifest?path=%2Fyaml%2Fmerge-build.yaml&version=GBc1%2F11%2Fmain&_a=contents

eos_build/scripts/merge.sh --variant mteos -sku default

eos_build/scripts/merge.sh -s test --variant mteos -sku default --osflavor userdebug



Note:
remove modem build from NHLOS
https://dev.azure.com/E-OS/device/_git/qcom-Lahaina.LA.1.0-premium-high-2020-spf-1-0_amss_standard_oem/commit/fa9d731f38550d5aa1556b4a20d6deb40bbb7888?refName=refs%2Fheads%2Fc1%2F11%2Fmain
