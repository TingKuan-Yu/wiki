# PR/Bugs
- https://dev.azure.com/E-OS/Zeta/_workitems/edit/103407
  - https://dev.azure.com/E-OS/device/_git/qcom-BOOT.MXF.1.0-premium-high-2020-spf-1-0_amss_standard_oem/commit/7ae03a1a67e134c937ea5883f7a6bbf9890ea7cd?refName=refs%2Fheads%2Fc1%2F11%2Fmain&path=%2Fboot_images%2Fboot%2FQcomPkg%2FSocPkg%2FLahaina%2FCommon%2Fuefiplat.cfg
  - https://dev.azure.com/E-OS/device/_git/caf-kernel.msm-5..4/commit/f05eb8a31af1211670d7ec129f5166a114e6ec29?refName=refs%2Fheads%2Fpersonal%2Ftingkuanyu%2F11%2Fkernel%2Fpon_telemetry
  - https://dev.azure.com/E-OS/device/_git/caf-kernel.msm-5..4/commit/f05eb8a31af1211670d7ec129f5166a114e6ec29?refName=refs%2Fheads%2Fpersonal%2Ftingkuanyu%2F11%2Fkernel%2Fpon_telemetry
  - https://dev.azure.com/E-OS/ssi/_git/platform.vendor.surface.integrationservice/pullrequest/25178

- https://dev.azure.com/E-OS/Zeta/_workitems/edit/159278

- https://dev.azure.com/E-OS/Zeta/_workitems/edit/158345/



# 8350 PMIC
- SM8350/SM7350/SM7325 PMIC Software User Guide
  - 80-PK177-100 Rev. J
- subtype: 8
- PMK8350 - SPMI_USID 0
- PM8350 - SPMI_USID 1
```
qcom,pm8350@1 {
	compatible = "qcom,spmi-pmic";
	reg = <1 SPMI_USID>;
```
- PM8350c - SPMI_USID 2
- PM8350b - SPMI_USID 3
```
qcom,pm8350b@3 {
	compatible = "qcom,spmi-pmic";
	reg = <3 SPMI_USID>;
```

# dump
- PMK8350: 0x800 to 0x8ff
```
To generate the PON PBS ADB dump, run the following commands:
adb root
adb shell
mount –t debugfs none /sys/kernel/debug
cd /sys/kernel/debug/regmap/spmi0-00
echo 0xFF > count
echo 0x800 > address
cat data
```

# patch
- https://dev.azure.com/E-OS/device/_git/caf-kernel.msm-5..4/commit/f05eb8a31af1211670d7ec129f5166a114e6ec29?refName=refs%2Fheads%2Fpersonal%2Ftingkuanyu%2F11%2Fkernel%2Fpon_telemetry
- [pmic_dump_telemetry_patch.tar.gz](/.attachments/pmic_dump_telemetry_patch.tar-dca396e1-c8ac-4802-9498-0bddffab4fba.gz)

# Test
```
c1:/sys/kernel/telemetry/poweron # cat pon_pmic_regs                                                                                                                                                              
PMK8350 Regs: 
 880:  0  0  0  0  0  0  0  0  0  0  0  0 30  0  0  0 
 890:  0 40  0  0 45 25  0  0  0 80 80  0  0  0  0  0 
 8a0:  0  0  0  0  0  0  0  0  0  0  0  0  0  0  0  0 
 8b0:  0  0  0  0  0  0  0  0  0  0  0  0  0  0  0  0 
 8c0:  0  0  0  0  0  0  0  0  8  8  0  0  0  0  0  0 
 8d0:  0  0  0  0  0  0  0  0  0  0  5  0  0  0  0  0 
 8e0:  0  0  0  0  0  0  0  0  0  0  0  0  0  0  0 80 
 8f0:  0  0  0  0  0  0  0  0  0  0  0  0  0  0  0  0 
PM8350 Regs: 
 880:  0  0  0  0 ea 80 8b 80  3  0  0  0  0  0  0  0 
 890:  0 40  0  0 45  0  0  0  0  0  0  0  0  0  0  0 
 8a0:  0  0  0  0  0  0  0  0  0  0  0  0  0  0  0  0 
 8b0:  0  0  0  0  0  0  0  0  0  0  0  0  0  0  0  0 
 8c0:  0  0  0  0  0  0  0 40  0  0  0  0  0  0  0  0 
 8d0:  0  0  0  0  0  0  0  0  0  0  5  0  0  0  0  0 
 8e0:  0  0  0  0  0  0  0  0  0  0  0  0  0  0  0 81 
 8f0:  0  0  0  0  0  0  0  0  0  0  0  0  0  0  0  0 
PM8350C Regs: 
 880:  0  0  0  0 e7 80 8b 80  3  0  0  0  0  0  0  0 
 890:  0 40  0  0 45  4  0  0  0  0  0  0  0  0  0  0 
 8a0:  0  0  0  0  0  0  0  0  0  0  0  0  0  0  0  0 
 8b0:  0  0  0  0  0  0  0  0  0  0  0  0  0  0  0  0 
 8c0:  0  0  0  0  0  0  0  0  8  0  0  0  0  0  0  0 
 8d0:  0  0  0  0  0  0  0  0  0  0  5  0  0  0  0  0 
 8e0:  0  0  0  0  0  0  0  0  0  0  0  0  0  0  0 80 
 8f0:  0  0  0  0  0  0  0  0  0  0  0  0  0  0  0  0 
PM8350B Regs: 
 880:  0  0  0  0 e7 80 8b 80  3  0  0  0  0  2  0  0 
 890:  0 40  0  0 45  0  0  0  0  0  0  0  0  0  0  0 
 8a0:  0  0  0  0  0  0  0  0  0  0  0  0  0  0  0  0 
 8b0:  0  0  0  0  0  0  0  0  0  0  0  0  0  0  0  0 
 8c0:  0  0  0  0  0  0  0  0  8  0  0  0  0  0  0  0 
 8d0:  0  0  0  0  0  0  0  0  0  0  5  0  0  0  0  0 
 8e0:  0  0  0  0  0  0  0  0  0  0  0  0  0  0  0 80 
 8f0:  0  0  0  0  0  0  0  0  0  0  0  0  0  0  0  0 
```