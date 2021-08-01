# pre study
- https://www.kernel.org/doc/Documentation/kbuild/kbuild.txt


# test environment
- files
```
tingkuanyu@TonyYuLinux1:/E/GKI/hlos_vendor/out/target/product/oemc1/dlkm/lib/test$ ls tmp/lib/modules/0.0/
clk-dummy.ko         crypto-qti-common.ko  icc-rpmh.ko                modules.dep          msm-poweroff.ko                 pinctrl-shima.ko      qnoc-lahaina.ko   rpmh-regulator.ko
clk-qcom.ko          crypto-qti-hwkm.ko    iommu-logger.ko            modules.dep.bin      phy-qcom-ufs.ko                 pinctrl-yupik.ko      qnoc-qos.ko       sdhci-msm.ko
clk-rpmh.ko          gcc-lahaina.ko        memory_dump_v2.ko          modules.devname      phy-qcom-ufs-qmp-v4-lahaina.ko  proxy-consumer.ko     qnoc-shima.ko     secure_buffer.ko
cmd-db.ko            gcc-shima.ko          modules.alias              modules.order        phy-qcom-ufs-qmp-v4-yupik.ko    qcom-arm-smmu-mod.ko  qnoc-yupik.ko     stub-regulator.ko
cqhci-crypto.ko      gcc-yupik.ko          modules.alias.bin          modules.softdep      phy-qcom-ufs-qrbtc-sdm845.ko    qcom-pdc.ko           qpnp-power-on.ko  ufshcd-crypto-qti.ko
cqhci-crypto-qti.ko  hwkm.ko               modules.builtin.alias.bin  modules.symbols      pinctrl-lahaina.ko              qcom_rpmh.ko          refgen.ko         ufs-qcom.ko
cqhci.ko             icc-bcm-voter.ko      modules.builtin.bin        modules.symbols.bin  pinctrl-msm.ko                  _qcom_scm.ko          rpmhpd.ko
```
- depmod -b tmp/
  - Ff we don't specify a correct folder, the depmod command reports fail.
```
tingkuanyu@TonyYuLinux1:/E/GKI/hlos_vendor/out/target/product/oemc1/dlkm/lib/test$ depmod -b tmp/
depmod: ERROR: could not open directory /E/GKI/hlos_vendor/out/target/product/oemc1/dlkm/lib/test/tmp//lib/modules/5.4.0-73-generic: No such file or directory
depmod: FATAL: could not search modules: No such file or directory
```
- depmod -b tmp/ 0.0
```
tingkuanyu@TonyYuLinux1:/E/GKI/hlos_vendor/out/target/product/oemc1/dlkm/lib/test$ depmod -b tmp/ 0.0
depmod: WARNING: could not open modules.builtin at /E/GKI/hlos_vendor/out/target/product/oemc1/dlkm/lib/test/tmp//lib/modules/0.0: No such file or directory
```

# depmod test result
- tested files: [module_load_test.tar.gz](/.attachments/module_load_test.tar-70561447-8df5-417e-a714-cddaecd38377.gz)
- without module order or module




