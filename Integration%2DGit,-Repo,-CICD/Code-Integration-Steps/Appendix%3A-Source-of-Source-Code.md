
# Source Code
## Qualcomm original Source Code
  - https://chipcode.qti.qualcomm.com/microsoft-corporation/snapdragon-premium-high-2020-spf-1-0_amss_standard_oem/tree/r1.0.c8_00005.9
    - **snapdragon-premium-high-2020-spf-1-0_amss_standard_oem**
       https://chipmaster2.qti.qualcomm.com/home2/git/microsoft-corporation/snapdragon-premium-high-2020-spf-1-0_amss_standard_oem.git
    - **CAF: LA.QSSI.11.0.R1**
      repo init -u https://source.codeaurora.org/quic/la/la/system/manifest.git -b release -m LA.QSSI.11.0.r1-11100-qssi.0.xml --repo-url=git://codeaurora.org/tools/repo.git --repo-branch=caf-stable
    - **CAF: LA.UM.9.14.R1**
      repo init -u https://source.codeaurora.org/quic/la/la/vendor/manifest.git -b release -m LA.UM.9.14.r1-15100-LAHAINA.0.xml --repo-url=git://codeaurora.org/tools/repo.git --repo-branch=caf-stable
    - **CAF: LE.UM.4.3.1.R1**
      repo init -u https://source.codeaurora.org/quic/le/le/manifest.git -b release -m LE.UM.4.3.1.r1-03700-genericarmv8-64.0.xml --repo-url=git://codeaurora.org/tools/repo.git --repo-branch=caf-stable

## CICD arranged Qualcomm original Source Code for MTP
- **manifest branch is hi2020/11/main**
  - https://dev.azure.com/E-OS/device/_wiki/wikis/Wiki/44270/Building-Locally-for-sm8350-mtp
  - NHLOS only
    - repo init -u ssh://ssh.dev.azure.com/v3/e-os/device/manifest -b **hi2020/11/main** -m **nhlos/nhlos.xml**

# Build MTP from Qualcomm Source Code
- https://dev.azure.com/tingkuanyu/TingKuanYuPrivate1/_wiki/wikis/TingKuanYuPrivate1.wiki/120/MTP8350
