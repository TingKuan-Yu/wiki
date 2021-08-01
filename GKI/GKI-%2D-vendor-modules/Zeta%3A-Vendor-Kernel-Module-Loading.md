# Insert modules by modprobe
---
## init.target.rc
- source
  - device/oemc1/oemc1/init.target.rc
- target
  - vendor/etc/init/hw/init.target.rc
- boot sequence: **early-init -> init -> late-init -> boot**
- code
```
on early-init
    exec u:r:vendor_modprobe:s0 -- /vendor/bin/vendor_modprobe.sh
    exec u:r:vendor_modprobe:s0 -- /vendor/bin/modprobe -a -d /vendor/lib/modules q6_pdr_dlkm q6_notifier_dlkm snd_event_dlkm apr_dlkm adsp_loader_dlkm q6_dlkm native_dlkm pinctrl_wcd_dlkm pinctrl_lpi_dlkm swr_dlkm platform_dlkm hdmi_dlkm stub_dlkm wcd_core_dlkm wsa883x_dlkm bolero_cdc_dlkm wsa_macro_dlkm va_macro_dlkm rx_macro_dlkm tx_macro_dlkm bt_fm_slim wcd938x_dlkm wcd938x_slave_dlkm swr_dmic_dlkm swr_haptics_dlkm machine_dlkm radio-i2c-rtc6226-qca mmc_core mmc_block sdhci sdhci-pltfm sdhci-msm cdsprm spi-hid camera/tmf8801


on boot
    #Load WLAN driver
    exec_background u:r:vendor_modprobe:s0 -- /vendor/bin/modprobe -a -d /vendor/lib/modules/ qca_cld3_wlan qca_cld3_qca6390
    exec_background u:r:vendor_modprobe:s0 -- /vendor/bin/modprobe -a -d /vendor/lib/modules/5.4-gki qca_cld3_wlan qca_cld3_qca6390
```
- /vendor/lib/modules only ko file
  - Build in QGKI kernel only. Not for GKI.
- Example of QGKI only kernel module.
  - 


# modules.blocklist.${TARGET_PRODUCT}
---
## device/qcom/kernelscripts/buildkernel.sh
- Flow copy_all_to_prebuilt ${KERNEL_BINS} --> copy_modules_to_prebuilt ${PREBUILT_OUT} 
  - in copy_modules_to_prebuilt 
```
	# Copy the modules.blocklist file
	set -x
	BLOCKLIST_FILE=${PWD}/device/qcom/kernelscripts/modules_blocklist/modules.blocklist.${TARGET_PRODUCT}
	if [ -f "${BLOCKLIST_FILE}" ]; then
		cp ${BLOCKLIST_FILE} ${KERNEL_MODULES_OUT}/modules.blocklist
		sed -i -e '/blocklist/ s/-/_/g' ${KERNEL_MODULES_OUT}/modules.blocklist
	fi
	set +x
```
- Block list is used to block module installation in vendor_modprobe.sh
```
xec u:r:vendor_modprobe:s0 -- /vendor/bin/vendor_modprobe.sh
```
- if the module is only for QGKI it shall be installed in
```
exec u:r:vendor_modprobe:s0 -- /vendor/bin/modprobe -a -d /vendor/lib/modules q6_pdr_dlkm q6_notifier_dlkm snd_event_dlkm apr_dlkm adsp_loader_dlkm q6_dlkm native_dlkm pinctrl_wcd_dlkm pinctrl_lpi_dlkm swr_dlkm platform_dlkm hdmi_dlkm stub_dlkm wcd_core_dlkm wsa883x_dlkm bolero_cdc_dlkm wsa_macro_dlkm va_macro_dlkm rx_macro_dlkm tx_macro_dlkm bt_fm_slim wcd938x_dlkm wcd938x_slave_dlkm swr_dmic_dlkm swr_haptics_dlkm machine_dlkm radio-i2c-rtc6226-qca mmc_core mmc_block sdhci sdhci-pltfm sdhci-msm cdsprm spi-hid camera/tmf8801
```
- If the module is for GKI and QGKI, it shall be installed later.
  - Example of wlan - block and load later
```
on boot
    #Load WLAN driver
    exec_background u:r:vendor_modprobe:s0 -- /vendor/bin/modprobe -a -d /vendor/lib/modules/ qca_cld3_wlan qca_cld3_qca6390
    exec_background u:r:vendor_modprobe:s0 -- /vendor/bin/modprobe -a -d /vendor/lib/modules/5.4-gki qca_cld3_wlan qca_cld3_qca6390
```

# Some strange modules
## only in QGKI and blocked and not be installed
- ./vendor/lib/modules/tda18218.ko
  - drivers/media/tuners/tda18218*
- mxl5007t
  -drivers/media/tuners/mxl5007t.*


## Both GKI and QGKI but not in block list
q6_pdr_dlkm.ko, q6_notifier_dlkm.ko, apr_dlkm.ko, adsp_loader_dlkm.ko, q6_dlkm.ko, native_dlkm.ko, pinctrl_wcd_dlkm, pinctrl_lpi_dlkm, swr_dlkm, platform_dlkm, stub_dlkm, wcd_core_dlkm, wsa883x_dlkm, bolero_cdc_dlkm, wsa_macro_dlkm, va_macro_dlkm, rx_macro_dlkm, tx_macro_dlkm, bt_fm_slim, wcd938x_dlkm, wcd938x_slave_dlkm, swr_dmic_dlkm, swr_haptics_dlkm, machine_dlkm

- target object
```
./vendor/lib/modules/5.4-gki/q6_pdr_dlkm.ko
./vendor/lib/modules/q6_pdr_dlkm.ko

./vendor/lib/modules/5.4-gki/q6_notifier_dlkm.ko
./vendor/lib/modules/q6_notifier_dlkm.ko

./vendor/lib/modules/5.4-gki/apr_dlkm.ko
./vendor/lib/modules/apr_dlkm.ko

:

```
- not in block list
- conclusion
  - no need set in on early-init "exec u:r:vendor_modprobe:s0 -- /vendor/bin/modprobe -a -d ..."
  - These module will be load in /vendor/bin/vendor_modprobe.sh


## Only QGKI hdmi_dlkm and not in the block list
- hdmi_dlkm.ko, radio-i2c-rtc6226-qca spi-hid tmf8801 
- target object
```
./vendor/lib/modules/hdmi_dlkm.ko

./vendor/lib/modules/radio-i2c-rtc6226-qca.ko

:
```
- conclusion
  - no need set in on early-init "exec u:r:vendor_modprobe:s0 -- /vendor/bin/modprobe -a -d ..."
  - These module will be load in /vendor/bin/vendor_modprobe.sh

## No build in for Zeta
-  mmc_core mmc_block sdhci-pltfm

## moved to vendor_boot both for GKI only
- sdhci.ko, sdhci-msm.ko, cdsprm
- target objects
```
./dlkm/lib/modules/gki/sdhci-msm.ko
./vendor-ramdisk/lib/modules/5.4-gki/sdhci-msm.ko
./vendor/lib/modules/5.4-gki/cdsprm.ko
```
- load in vendor-boot
