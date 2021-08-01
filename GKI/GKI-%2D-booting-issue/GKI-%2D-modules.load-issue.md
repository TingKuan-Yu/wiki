# Task
- https://dev.azure.com/E-OS/Zeta/_workitems/edit/171872

```
tingkuanyu@TonyYuLinux1:/E/GKI/kernel/out/target/product/oemc1/dlkm/lib/modules/gki$ cd /E/tmp/
tingkuanyu@TonyYuLinux1:/E/tmp$ ls
clk-dummy.ko     cqhci-crypto-qti.ko   gcc-shima.ko      iommu-logger.ko                 phy-qcom-ufs-qmp-v4-yupik.ko  pinctrl-yupik.ko      _qcom_scm.ko     qpnp-power-on.ko   secure_buffer.ko
clk-qcom.ko      cqhci.ko              gcc-yupik.ko      memory_dump_v2.ko               phy-qcom-ufs-qrbtc-sdm845.ko  proxy-consumer.ko     qnoc-lahaina.ko  refgen.ko          stub-regulator.ko
clk-rpmh.ko      crypto-qti-common.ko  hwkm.ko           msm-poweroff.ko                 pinctrl-lahaina.ko            qcom-arm-smmu-mod.ko  qnoc-qos.ko      rpmhpd.ko          ufshcd-crypto-qti.ko
cmd-db.ko        crypto-qti-hwkm.ko    icc-bcm-voter.ko  phy-qcom-ufs.ko                 pinctrl-msm.ko                qcom-pdc.ko           qnoc-shima.ko    rpmh-regulator.ko  ufs-qcom.ko
cqhci-crypto.ko  gcc-lahaina.ko        icc-rpmh.ko       phy-qcom-ufs-qmp-v4-lahaina.ko  pinctrl-shima.ko              qcom_rpmh.ko          qnoc-yupik.ko    sdhci-msm.ko
tingkuanyu@TonyYuLinux1:/E/tmp$ mkdir /D/tmp
tingkuanyu@TonyYuLinux1:/E/tmp$ zip -r test.zip clk-dummy.ko     cqhci-crypto-qti.ko   gcc-shima.ko      iommu-logger.ko                 phy-qcom-ufs-qmp-v4-yupik.ko 
  adding: clk-dummy.ko (deflated 78%)
  adding: cqhci-crypto-qti.ko (deflated 76%)
  adding: gcc-shima.ko (deflated 84%)
  adding: iommu-logger.ko (deflated 80%)
  adding: phy-qcom-ufs-qmp-v4-yupik.ko (deflated 74%)
tingkuanyu@TonyYuLinux1:/E/tmp$ unzip test.zip -d unzip
Archive:  test.zip
  inflating: unzip/clk-dummy.ko      
  inflating: unzip/cqhci-crypto-qti.ko  
  inflating: unzip/gcc-shima.ko      
  inflating: unzip/iommu-logger.ko   
  inflating: unzip/phy-qcom-ufs-qmp-v4-yupik.ko  
tingkuanyu@TonyYuLinux1:/E/tmp$ unzip test.zip -d /D/tmp/unzip
Archive:  test.zip
  inflating: /D/tmp/unzip/clk-dummy.ko  
  inflating: /D/tmp/unzip/cqhci-crypto-qti.ko  
  inflating: /D/tmp/unzip/gcc-shima.ko  
  inflating: /D/tmp/unzip/iommu-logger.ko  
  inflating: /D/tmp/unzip/phy-qcom-ufs-qmp-v4-yupik.ko  
tingkuanyu@TonyYuLinux1:/E/tmp$ find unzip/
unzip/
unzip/gcc-shima.ko
unzip/cqhci-crypto-qti.ko
unzip/iommu-logger.ko
unzip/phy-qcom-ufs-qmp-v4-yupik.ko
unzip/clk-dummy.ko
tingkuanyu@TonyYuLinux1:/E/tmp$ find /D/tmp/unzip/
/D/tmp/unzip/
/D/tmp/unzip/clk-dummy.ko
/D/tmp/unzip/iommu-logger.ko
/D/tmp/unzip/phy-qcom-ufs-qmp-v4-yupik.ko
/D/tmp/unzip/cqhci-crypto-qti.ko
/D/tmp/unzip/gcc-shima.ko
```