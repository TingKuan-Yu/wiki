- bootable flow
proxy-consumer.ko
clk-qcom.ko
clk-dummy.ko
cqhci-crypto.ko
cqhci.ko
qcom-pdc.ko
pinctrl-msm.ko
hwkm.ko
crypto-qti-hwkm.ko
pinctrl-yupik.ko
cmd-db.ko
qcom_rpmh.ko
icc-bcm-voter.ko
qpnp-power-on.ko
clk-rpmh.ko
_qcom_scm.ko
secure_buffer.ko
gcc-yupik.ko
memory_dump_v2.ko
qnoc-qos.ko
icc-rpmh.ko
qnoc-yupik.ko
iommu-logger.ko
refgen.ko
crypto-qti-common.ko
ufshcd-crypto-qti.ko
qnoc-lahaina.ko
msm-poweroff.ko
phy-qcom-ufs.ko
phy-qcom-ufs-qrbtc-sdm845.ko
phy-qcom-ufs-qmp-v4-yupik.ko
qcom-arm-smmu-mod.ko
qnoc-shima.ko
rpmh-regulator.ko
stub-regulator.ko
gcc-lahaina.ko
cqhci-crypto-qti.ko
ufs-qcom.ko
pinctrl-lahaina.ko
surfacedisplay.ko
msm_drm.ko
qcom_edac.ko
sdhci-msm.ko
phy-qcom-ufs-qmp-v4-lahaina.ko
gcc-shima.ko
pinctrl-shima.ko
rpmhpd.ko

- with uart
From Mark:
但是pinctrl load之前要先load前面那三個 然後qcon一定要在pinctrl后...

Tony Yu David Shih 在目前的module.load上在最前面加上這個順序就可以用有uart的kernel看到uart，不過開不進去，但不會當掉，我想如果只是要看stage2的load module失敗的原因應該還可以 gcc-lahaina.ko qcom-pdc.ko rpmh-regulator.ko pinctrl-lahaina.ko qnoc-lahaina.ko...

gcc-lahaina.ko
qcom-pdc.ko
rpmh-regulator.ko
pinctrl-lahaina.ko
qnoc-lahaina.ko