**Code Integration: LA 1.0_C8 Post Post-CS (r1.0.C8_0004.7): Snapdragon_Premium_High_2020.SPF.1.0.c8)**


[[_TOC_]]

# Internal Reference
1. https://dev.azure.com/DSQO-Taipei/Knowledge%20Share/_wiki/wikis/Knowledge-Share.wiki/83/Code-integration
2. https://dev.azure.com/e-os/device/_git/artifacts.merge?path=%2Fpackages-crs-customer.json&version=GBc1%2F11%2Fmain&_a=contents
3. https://dev.azure.com/e-os/device/_git/manifest?path=%2Fprojects%2Fprojects-nhlos-device-qcom.xml
4. ADO:
   - Hi 2020, Int, 11, C8_00005.9: https://dev.azure.com/E-OS/device/_git/manifest?path=%2Fcaf%2FLA.UM.9.14.r1-15100-LAHAINA.0.ado.xml&version=GBhi2020%2Fint%2F11%2Fc8_00005.9

# QC Reference
1. QC Tracker: https://nam06.safelinks.protection.outlook.com/ap/x-59584e83/?url=https%3A%2F%2Fmicrosoft-my.sharepoint.com%2F%3Ax%3A%2Fp%2Faditshah%2FETpdEwk3Q-FNtVGZ1jLHxqUBKoNznHC4EfB4LUkPGG462w%3Fe%3DM45fgw&data=04%7C01%7Cbert.chen%40microsoft.com%7C8bd9e84f21d541e2c53608d8eb18f4bb%7C72f988bf86f141af91ab2d7cd011db47%7C0%7C0%7C637517839771595168%7CUnknown%7CTWFpbGZsb3d8eyJWIjoiMC4wLjAwMDAiLCJQIjoiV2luMzIiLCJBTiI6Ik1haWwiLCJXVCI6Mn0%3D%7C1000&sdata=0sS6tCTMBPz4d9A7DGfvfdLbfguudkqmGmm98OpN9hY%3D&reserved=0
   - Release: 3/11, 3/25, 4/8, 4/22, 5/6

2. Source Code: https://chipcode.qti.qualcomm.com/microsoft-corporation/snapdragon-premium-high-2020-spf-1-0_amss_standard_oem/tree/r1.0.c8_00005.9
   - (1). about.html
   - (2). Build:
	Software Product Family	Distribution	Context	ECCN	Serial Number
	Snapdragon_Premium_High_2020.SPF.1.0	N/A 0.0.005.9	OEM	5D002.c.1	288152
   - (3). Build Components:
	 - Product(s)	Image	Build/Label	Distro Path	Format
	 - Cedros.LA.1.0.c1, Lahaina.LA.1.0.c8	ADSP.HT.5.5	ADSP.HT.5.5-00769.5-LAHAINA-3	ADSP.HT.5.5	SRC
	 - Cedros.LA.1.0.c1, Lahaina.LA.1.0.c8	AOP.HO.3.0	AOP.HO.3.0-00317-LAHAINA_E-1	AOP.HO.3.0	SRC
	 - Cedros.LA.1.0.c1, Lahaina.LA.1.0.c8	BOOT.MXF.1.0	BOOT.MXF.1.0-00682-LAHAINA-1	BOOT.MXF.1.0	SRC_LAHAINA_LAA
	 - Lahaina.LA.1.0.c8	BTFM.HSP.1.0.0	BTFM.HSP.1.0.0-00858-QCAHSPROMZ-1	BTFM.HSP.1.0.0	BIN
	 - Cedros.LA.1.0.c1	BTFW.HSP.2.0.0	BTFW.HSP.2.0.0-00556-HSP_PATCHZ-1	BTFW.HSP.2.0.0	BIN
	 - Cedros.LA.1.0.c1, Lahaina.LA.1.0.c8	CDSP.HT.2.5	CDSP.HT.2.5-00764.1-LAHAINA-1	CDSP.HT.2.5	SRC
	 - Cedros.LA.1.0.c1, Lahaina.LA.1.0.c8	CPUCP.FW.1.0	CPUCP.FW.1.0-00054-LAHAINA.EXT-1	CPUCP.FW.1.0	BIN
	 - Lahaina.LA.1.0.r1	CVP.VPU.2.0	CVP.VPU.2.0-00007-PROD-1*	CVP.VPU.2.0	BIN
	 - CEDROS.LA.1.0.C1	Cedros.LA.1.0.c1-00006-STD.PROD-1	Cedros.LA.1.0	SRC
	 - Cedros.LA.1.0.c1, Lahaina.LA.1.0.c8	LA.QSSI.11.0.R1	LA.QSSI.11.0.r1-11100-qssi.0-1	LA.QSSI.11.0	SRC
	 - Cedros.LA.1.0.c1, Lahaina.LA.1.0.c8	LA.UM.9.14.R1	LA.UM.9.14.r1-15100-LAHAINA.0-1	LA.UM.9.14	SRC
	 - Cedros.LA.1.0.c1, Lahaina.LA.1.0.c8	LE.UM.4.3.1.R1	LE.UM.4.3.1.r1-03700-genericarmv8-64.0-1	LE.UM.4.3.1	SRC
	 - LAHAINA.LA.1.0.C8	Lahaina.LA.1.0.c8-00020-STD.PROD-2	Lahaina.LA.1.0	SRC
	 - Cedros.LA.1.0.c1, Lahaina.LA.1.0.c8	MPSS.HI.4.0	MPSS.HI.4.0-01680.1-LC_ALL_PACK-1	MPSS.HI.4.0	SRC-Modem-Standard
	 - Lahaina.LA.1.0.c8	SLPI.HY.4.0	SLPI.HY.4.0-00193-LAHAINA-1*	SLPI.HY.4.0	SRC
	 - Lahaina.LA.1.0.c8	SPSS.A1.1.4	SPSS.A1.1.4-00099-LAHAINA.0-1*	SPSS.A1.1.4	BIN
	 - Lahaina.LA.1.0.r1	TZ.APPS.1.0	TZ.APPS.1.0-00236.1-SPF.LAHAINA-1*	TZ.APPS.1.0	BIN
	 - Cedros.LA.1.0.c1, Lahaina.LA.1.0.c8	TZ.APPS.2.0	TZ.APPS.2.0-00152-SPF.LAHAINA-1	TZ.APPS.2.0	BIN
	 - Lahaina.LA.1.0.r1	TZ.XF.5.0	TZ.XF.5.0-03426.3-SPF.LAHAINA-1*	TZ.XF.5.0	BIN
	 - Cedros.LA.1.0.c1, Lahaina.LA.1.0.c8	TZ.XF.5.11	TZ.XF.5.11-00306-SPF.LAHAINA-1	TZ.XF.5.11	BIN
	 - Lahaina.LA.1.0.r1	VIDEO.VPU.2.0	VIDEO.VPU.2.0-00014-PROD-1*	VIDEO.VPU.2.0	BIN
	 - Lahaina.LA.1.0.r1	WIGIG.TLN.1.0	WIGIG.TLN.1.0-01295-WIGIGTLNZ-1*	WIGIG.TLN.1.0	BIN
	 - Cedros.LA.1.0.c1, Lahaina.LA.1.0.c8	WLAN.HSP.1.1.C3	WLAN.HSP.1.1.c3-00107-QCAHSPSWPL_V1_V2_SILICONZ-1	WLAN.HSP.1.1	BIN

# Code Integration
## 0. Prepare
   - Wiki Update for c8_00005.9: https://dev.azure.com/DSQO-Taipei/Knowledge%20Share/_wiki/wikis/Knowledge-Share.wiki/125/c8_00005.9
   - Binary Check List: https://microsoft-my.sharepoint.com/:x:/p/fangruwu/EYBwnapBqa5BuQbPQpxC8GIBcNo4_jHsziaMK4Fo3UEKKQ
   - Major AOD Resources - Pipelines & Artifacts 
     - https://dev.azure.com/tingkuanyu/TingKuanYuPrivate1/_wiki/wikis/TingKuanYuPrivate1.wiki?wikiVersion=GBwikiMaster&pagePath=%2FIntegration%252DGit%2C%20Repo%2C%20CICD%2FCapatian%20Bert%2FMajor%20AOD%20Resources%20%252D%20Pipelines%20%26%20Artifacts&pageId=206&_a=edit


## 1. Notes:
 - LA: Linux Android
 - LE: Linux Embedded
 - CAF: Code Aurora Forum
   - A. https://www.codeaurora.org/projects/linux-msm
   - B. Linux MSM
 - ADO: Azure DevOps
 - QSSI: Qualcomm Single System Image
 - SSI: Surface System Image
 - UM: ???
 - Yocto Project: To produce tools and processes that enable the creation of Linux distributions for embedded and IoT software.
 - WiGig: Wireless Gigabit Alliance
 - MSM: Mobole Station Modems
 - FSM: Femtocell Station Modems
   - A. Femto + Cell
   - B. Femto (symbol f): 10^-15
 - NFC: Near Field Communication
 - Ant: Apache Ant, software tool for automating software build processes
 - Version Info:
   LA.QSSI.11.0.r1-11100-qssi.0-1
   LA.UM.9.14.r1-15100-LAHAINA.0-1
   LE.UM.4.3.1.r1-03700-genericarmv8-64.0-1
 - Tag:
   r1.0.c8_00005.9,LA.QSSI.11.0.r1-11100-qssi.0,LA.UM.9.14.r1-15100-LAHAINA.0


## 2. Add info page (c8_00005.9) -> Added by Bert
- https://dev.azure.com/DSQO-Taipei/Knowledge%20Share/_wiki/wikis/Knowledge-Share.wiki/100/Code-Integration-version

## 3. (Done by ) Send email -> Done by Ken (03/18/2021)
- To subsystem about which version of binry files they perfer to use
- https://microsoft-my.sharepoint.com/:x:/p/fangruwu/EYBwnapBqa5BuQbPQpxC8GIBcNo4_jHsziaMK4Fo3UEKKQ?e=sLAHCG

## 4. Create manifest for QC release -> Done by Neel
- https://dev.azure.com/DSQO-Taipei/Knowledge%20Share/_wiki/wikis/Knowledge-Share.wiki/123/Special-case-for-creating-branchf
- Contents.xml: https://dev.azure.com/E-OS/qcom/_git/Lahaina.LA.1.0-premium-high-2020-spf-1-0_amss_standard_oem?path=%2Fcontents.xml&version=GTr1.0.c8_00005.9&_a=contents
- QC Website: https://chipcode.qti.qualcomm.com/microsoft-corporation/snapdragon-premium-high-2020-spf-1-0_amss_standard_oem/tree/r1.0.c8_00005.9
- Download XML from QC Release:
  - A. la.system.manifest
    https://dev.azure.com/E-OS/caf/_git/la.system.manifest
  - B. manifest
    https://dev.azure.com/E-OS/caf/_git/la.vendor.manifest
  - C. le.manifest
    https://dev.azure.com/E-OS/caf-private_le/_git/le.manifest
- Create caf xml:
  - A. Script:
    https://dev.azure.com/E-OS/cicd/_git/scripts
  - B. cmd example：
    - python3 /mnt/Second/build_script/scripts/user/tjr/merge/update-manifest.py /mnt/Second/code-integration/17/origin/LA.QSSI.11.0.r1-08600-qssi.0.xml /mnt/Second/code-integration/17/modified/LA.QSSI.11.0.r1-08600-qssi.0.ado.xml caf caf-qssi
    - python3 /mnt/Second/build_script/scripts/user/tjr/merge/update-manifest.py /mnt/Second/code-integration/17/origin/LA.UM.9.14.r1-12000-LAHAINA.0.xml /mnt/Second/code-integration/17/modified/LA.UM.9.14.r1-12000-LAHAINA.0.ado.xml caf-private_LA.UM.9.14 caf
    - python3 /mnt/Second/build_script/scripts/user/tjr/merge/update-manifest.py /mnt/Second/code-integration/17/origin/LE.UM.4.3.1.r1-03100-genericarmv8-64.0.xml /mnt/Second/code-integration/17/modified/LE.UM.4.3.1.r1-03100-genericarmv8-64.0.ado.xml caf-private_le caf-le

## 5. Special Cases for Creating Int Branch -> Done by Amy (03/31/2021)
- https://dev.azure.com/DSQO-Taipei/Knowledge%20Share/_wiki/wikis/Knowledge-Share.wiki/123/Special-case-for-creating-branch
- repo_category:
  class RepoCategory(Enum):
      VENDOR = "vendor"
      KERNEL = "kernel"
      QSSI = "system"
      NHLOS = "nhlos"
      MERGE = "merge"
      SSI = "ssi"
- Special Cases
  - A. Different Path
  - B. Change Repo
  - C. Repo with Multiple Tag
  - D. SSI Repo which Needs to be Chnaged

## 6. Create Int Branch
- Run pipeline step 1 "create repo list" and step 2 "create branch for int branch"
  - https://dev.azure.com/DSQO-Taipei/Knowledge Share/_wiki/wikis/Knowledge-Share.wiki/84/Apply-patches-with-automation-pipeline
- If you meet any error about multi-tag during creating int branch, it need to check which tag need to be use and create it manually
  - https://dev.azure.com/DSQO-Taipei/Knowledge Share/_wiki/wikis/Knowledge-Share.wiki/93/Create-int-branch-Manual

## 7. Create Manifest for MS code and necessary repo
  - https://dev.azure.com/DSQO-Taipei/Knowledge Share/_wiki/wikis/Knowledge-Share.wiki/86/Some-important-repo-need-to-be-noticed-in-code-integration-flow
  - Create New Manifest
    - A. Template (Personal):
      https://dev.azure.com/e-os/device/_git/manifest?version=GBpersonal%2Fbert%2Fc1-int-11-c8_00005.9
      https://dev.azure.com/e-os/device/_git/manifest?version=GBpersonal%2Fbert%2Fqssi-int-11-c8_00005.9
      https://dev.azure.com/e-os/ssi/_git/manifest?version=GBpersonal%2Fbert%2Fssi-int-11-c8_00005.9
    - B. Download Manifest from c1/11/main, qssi/11/main, and ssi/11/main
      git clone git@ssh.dev.azure.com:v3/E-OS/device/manifest -b c1/11/main
      git clone git@ssh.dev.azure.com:v3/E-OS/device/manifest -b qssi/11/main
      git clone git@ssh.dev.azure.com:v3/E-OS/ssi/manifest -b ssi/11/main
    - C. Replace files in caf folder
      LA.QSSI.11.0.r1-11100-qssi.0.ado.xml
      LA.UM.9.14.r1-15100-LAHAINA.0.ado.xml
      LE.UM.4.3.1.r1-03700-genericarmv8-64.0.ado.xml
    - D. Compare with Hi2020 to figure out the diff
    - E. General Changes for All:
      - a. LA.QSSI.11.0.r1-09600 -> LA.QSSI.11.0.r1-11100
           projects-kernel-common.xml
           projects-kernel-specific.xml
           merg.xml
           vendor-core.xml
      - b. LA.UM.9.14.r1-12800 -> LA.UM.9.14.r1-15100
           projects-kernel-specific.xml
           vendor-core.xml
      - c. LE.UM.4.3.1.r1-03200 -> LE.UM.4.3.1.r1-03700
           remotes.xml
           le.xml
           nhlos.xml
      - d. Cedros.LA.1.1 -> Cedros.LA.1.0
           projects-nhlos-qcom.xml
           projects-nhlos-device-qcom.xml
      - e. Lahaina.LA.1.1 -> Lahaina.LA.1.0 (replace command: grep -rli 'Lahaina.LA.1.1' * | xargs -i@ sed -i 's:Lahaina.LA.1.1:Lahaina.LA.1.0:g' @)
           - projects-nhlos-qcom.xml
           - projects-nhlos-device-qcom.xml
           - apdp-build.yaml
           - tz.apps-build.yaml
           - slpi-build.yaml
           - boot-build.yaml
           - File Name (Not Chnaged Yet UNTIL into the Main):
             qcom-Lahaina.LA.1.1-premium-high-2020-spf-1-0_amss_standard_oem-pr.yaml
           - ymal in PR folder:
             artificats.nhlos-pr.yaml
             priv-la.9.14-abl.tianocore.edk2-pr.yaml
             qcom-Lahaina.LA.1.1-premium-high-2020-spf-1-0_amss_standard_oem-pr.yaml
             qcom-SLPI.HY.4.0-xxx.yaml
             qcom-CPUCP.FW.1.0-xxx.yaml
             qcom-MPSS.HI.4.0-xxx.yaml
             qcom-TZ.XF.5.0-xxx.yaml
             qcom-ADSP.HT.5.5-xxx.yaml
             qcom-BOOT.MXF.1.0-xxx.yaml
             qcom-BTMF.HSP.1.0-xxx.yaml
             qcom-CDSP.HT.2.5-xxx.yaml
             qcom-WLAN.HSP.1.1-xxx.yaml
             qcom-AOP.HO.3.0-xxx.yaml
     - f. Change Use Build Cache as FALSE
     - g. Change r1_00020.2 to c8_00005.9
     - h. Change Scheduled Rolling Builds as FALSE
     - i. Change the revision
       - For example
         (i). In project-kernel-common.xml, it uses LA.QSSI.11.0.r1-11100, the revision for kernel/configs path has bee changed.
         (ii). In project-kernel-specific.xml, it uses LA.UM.9.14.r1-15100, the revision for kernel/msm-5.4/techpack/dataipa path has bee changed.
       - Search the file names in caf to see which file inlcude the projects with path and revision from them
       - Search the path from caf to check if the revision is changed
  - For c1/11/main (in E-OS/device/manifest) with hi2020/int/11/c8_00005.9
    - Ref: https://dev.azure.com/E-OS/device/_git/manifest/commit/c1dfb6a5efcde812f1cd78d17e7080d01e3b07e0?refName=refs%2Fheads%2Fc1%2Fint%2F11%2Fr00020.2
    - Change c1/11/main to c1/int/11/c8_00005.9 in remotes.xml, but not for met-fos and eos_tools
    - Remove caf-ype/platform.vendor.opensource.sched from vendor-core.xm
  - For qssi/11/main (in E-OS/device/manifest) with hi2020-qssi/int/11/c8_00005.9
    - https://dev.azure.com/E-OS/device/_git/manifest/commit/8b0da7cedbd546f24060712e5fc76977a9567f4f?refName=refs%2Fheads%2Fc1-qssi%2Fint%2F11%2Fr00020.2
    - Change qssi/11/main to c1-qssi/int/11/c8_00005.9 and c1/11/main to c1/int/11/c8_00005.9 in createPrPipelineQssi.yaml and createPrYamlQssi.yaml
    - Change refs/heads/qssi/11/main to refs/heads/qssi/int/11/c8_00005.9 (replace command: grep -rli 'refs/heads/qssi/11/main' * | xargs -i@ sed -i 's:refs/heads/qssi/11/main:refs/heads/qssi/int/11/c8_00005.9:g' @)
    - Change refs/heads/c1-qssi/11/main to refs/heads/c1-qssi/int/11/c8_00005.9
  - For ssi/11/main (in E-OS/ssi/manifest), no hi2020
    - Ref: https://dev.azure.com/E-OS/ssi/_git/manifest/commit/3bda1586b4b76aaeeea46cf68585f9fe0516a1cc?refName=refs%2Fheads%2Fssi%2Fint%2F11%2Fr00020.2&path=%2Fremotes.xml
    - Change ssi/11/main to ssi/int/11/c8_00005.9 in remotes.xml for ssi-qcom
    - Add new ssi-int in remotes.xml
    - Rename ssi to ssi-int for device.surface.ssi in projects-ssi.xml
    - Change Source from cron-ssi-11-main-merge to cron-ssi-int-11-merge in merge-manifest.yaml
    - Change ssi/11/main to ssi/int/11/c8_00005.9 in vars.yaml
    - Change ssi-11-main-* to ssi-int-11-*  for Artifact Feeds in vars.yaml
  - Create official manifest branches
    - For c1/int/11/c8_00005.9, c1-qssi/int/11/c8_00005.9, and ssi/int/11/c8_00005.9
    - Check-in

## 8. Apply Int Pipeline
- https://dev.azure.com/e-os/device/_build?definitionScope=%5Ccode-integration
- Code-integration
  - create-repo-list
  - create-branch
- create-patch
  - Branch / tag: bsp/code-integration
  - Tag Patch Feed:
  - Base Feed Version:
  - Latest Feed Version:
  - first / middle / last
- apply-patch
  - Branch / tag: bsp/code-integration
  - All Patch Feed:
- run-pipline-build

## 9. Create Int Branch
- Vendor:
  repo init -u ssh://ssh.dev.azure.com/v3/e-os/device/manifest -b c1/int/11/c8_00005.9 -m hlos.xml
  repo sync -c --no-tags --no-clone-bundle -j 2 --fail-fast --prune
- Kernel:
  repo init -u ssh://ssh.dev.azure.com/v3/e-os/device/manifest -b c1/int/11/c8_00005.9 -m kernel.xml
  repo sync -c --no-tags --no-clone-bundle -j 2 --fail-fast --prune
- NHLOS:
  repo init -u ssh://ssh.dev.azure.com/v3/e-os/device/manifest -b c1/int/11/c8_00005.9 -m nhlos/nhlos.xml
  repo sync -c --no-tags --no-clone-bundle -j 2 --fail-fast --prune
- System:
  repo init -u ssh://ssh.dev.azure.com/v3/e-os/device/manifest -b c1-qssi/int/11/c8_00005.9 -m system.xml
  repo sync -c --no-tags --no-clone-bundle -j 2 --fail-fast --prune
- SSI:
  repo init -u ssh://ssh.dev.azure.com/v3/e-os/ssi/manifest -b ssi/int/11/c8_00005.9 -m system.xml
  repo sync -c --no-tags --no-clone-bundle -j 2 --fail-fast --prune
- Merge:
  repo init -u ssh://ssh.dev.azure.com/v3/e-os/device/manifest -b c1/int/11/c8_00005.9 -m merge.xml
  repo sync -c --no-tags --no-clone-bundle -j 2 --fail-fast --prune

## 10. Create Patch
- Create Repo List (create-repo-list pipeline)
  - Select a cloud build
  - Find the buildid for ssi and qssi
  - Run this pipeline with buildids and bsp/code-integration branch
  - first = Tag + Latest, middle = Base + Latest, last = Base + HEAD
  - Completed, get version
- Create Patch (create-patch pipeline)
  - Run this pipeline with feed version, last version and current version, and bsp/code-integration branch
  - Atrifacts -> code-integration -> c1-patch

## 11. Apply Patch
- XML Info: https://microsoft-my.sharepoint.com/:x:/p/fangruwu/EVJYq4P479NPo_Wy68-yi6sBLPniYhFEJ8J4TZwSBhQhXA
- Apply Patch (apply-patch pipeline)
  - Run this pipeline with version and bsp/code-integration branch
  - Atrifacts -> code-integration -> c1-apply
  - Completed, check apply_result.xlsx in Pulished -> apply_result
- Patches: https://dev.azure.com/E-OS/device/_packaging?_a=feed&feed=code-integration
  - First Patch: https://dev.azure.com/E-OS/device/_packaging?_a=package&feed=code-integration&package=c1-apply&protocolType=UPack&version=2021.406.1
  - Second Patch: https://dev.azure.com/E-OS/device/_packaging?_a=package&feed=code-integration&package=c1-apply&version=2021.408.1&protocolType=UPack
  - 3rd Patch: https://dev.azure.com/E-OS/device/_packaging?_a=package&feed=code-integration&package=c1-apply&version=2021.412.1&protocolType=UPack
  - 4th Patch: https://dev.azure.com/E-OS/device/_packaging?_a=package&feed=code-integration&package=c1-apply&protocolType=UPack&version=2021.413.1
  - 5th Patch (RC): https://dev.azure.com/E-OS/device/_packaging?_a=package&feed=code-integration&package=c1-apply&version=2021.414.1&protocolType=UPack
    - No changes in manifest for c1/11/main, qssi/11/main, and ssi/11/main
    - create-repo-list: c1/11/main cloud build, ssi: 2021.414.10 (buildid: 570270), qssi: 2021.414.9 (buildid: 57016) -> int: 2021.414.1, https://dev.azure.com/e-os/device/_build/results?buildId=570458&view=artifacts&pathAsName=false&type=publishedArtifacts
    - create-patch: Middle = 2021.413.1 + 2021.414.1 -> https://dev.azure.com/e-os/device/_build/results?buildId=570478&view=artifacts&pathAsName=false&type=publishedArtifacts
    - apply-patch: 2021.414.1 -> 
      https://dev.azure.com/E-OS/device/_build/results?buildId=570482&view=artifacts&pathAsName=false&type=publishedArtifacts
      https://dev.azure.com/E-OS/device/_packaging?_a=package&feed=code-integration&package=c1-apply&version=2021.414.1&protocolType=UPack
    - run-pipeline-build ->
      - (1). Branch/tag: bsp/code-integration
      - (2). Manifest Branch: c1/int/11/c8_00005.9
      - (3). QSSI Manifest Branch: c1-qssi/int/11/c8_00005.9
      - (4). SSI Manifest Branch: ssi/int/11/c8_00005.9
             Combo: https://dev.azure.com/e-os/device/_packaging?_a=package&feed=c1-int-11-images%40Local&package=c1-11-developer-combo&protocolType=UPack&version=2021.414.11
	     EDL: https://dev.azure.com/e-os/device/_packaging?_a=package&feed=c1-int-11-images%40Local&package=c1-11-developer-edl&protocolType=UPack&version=2021.414.11
  - 6th Patch (Last Diff): https://dev.azure.com/E-OS/device/_packaging?_a=package&feed=code-integration&package=c1-apply&version=2021.415.2&protocolType=UPack
    - No changes in manifest for c1/11/main, qssi/11/main, and ssi/11/main
    - create-repo-list: c1/11/main cloud build, ssi: 2021.415.10 (buildId=572659), qssi: 2021.414.8 (buildId=572551) -> int: 2021.415.1, https://dev.azure.com/e-os/device/_build/results?buildId=572693&view=artifacts&pathAsName=false&type=publishedArtifacts
    - create-patch: Middle = 2021.414.1 + 2021.415.1 ->
      - https://dev.azure.com/e-os/device/_build/results?buildId=572752&view=artifacts&pathAsName=false&type=publishedArtifacts
      - https://dev.azure.com/E-OS/device/_packaging?_a=package&feed=code-integration&package=c1-apply&version=2021.415.2&protocolType=UPack
    - Download Patch and Remove WLAN Patch: BDF V15 update (18b3c586)
      - https://dev.azure.com/e-os/device/_packaging?_a=package&feed=code-integration&package=c1-patch&protocolType=UPack&version=2021.415.1
      - Download:
        - az artifacts universal download --organization "https://dev.azure.com/E-OS/" --feed "code-integration" --name "c1-patch" --version "2021.415.1" --path .
      - Remove BDF V15 update for WLAN
      - Update a new version to 2021.415.2
	az artifacts universal publish --organization https://dev.azure.com/E-OS/  --scope organization --feed "code-integration" --name c1-patch --version "2021.415.2" --description "Parse from latest 2021.415.1 base 2021.414.1 tag 2021.414.1 and remove BDF V15 update for WLAN" --path <patch>
    - apply-patch: 2021.415.2 -> https://dev.azure.com/e-os/device/_build/results?buildId=572785&view=artifacts&pathAsName=false&type=publishedArtifacts
    - run-pipeline-build ->
      - (1). Branch/tag: bsp/code-integration
      - (2). Manifest Branch: c1/int/11/c8_00005.9
      - (3). QSSI Manifest Branch: c1-qssi/int/11/c8_00005.9
      - (4). SSI Manifest Branch: ssi/int/11/c8_00005.9
        - Combo: https://dev.azure.com/e-os/device/_packaging?_a=package&feed=c1-int-11-images%40Local&package=c1-11-developer-combo&protocolType=UPack&version=2021.415.12					
        - Combo: https://dev.azure.com/e-os/device/_packaging?_a=package&feed=c1-int-11-images%40Local&package=c1-11-developer-combo&protocolType=UPack&version=2021.415.12
        - EDL: https://dev.azure.com/e-os/device/_packaging?_a=package&feed=c1-int-11-images%40Local&package=c1-11-developer-edl&protocolType=UPack&version=2021.415.12					
        - Combo: https://dev.azure.com/e-os/device/_packaging?_a=package&feed=c1-int-11-images%40Local&package=c1-11-developer-combo&protocolType=UPack&version=2021.415.12

## 12. Set Artifact for Pipeline
- a. https://dev.azure.com/DSQO-Taipei/Knowledge%20Share/_wiki/wikis/Knowledge-Share.wiki/86/Some-important-repo-need-to-be-noticed-in-code-integration-flow
- b. https://dev.azure.com/DSQO-Taipei/Knowledge Share/_wiki/wikis/Knowledge-Share.wiki/75/How-to-set-up-a-cloud-build-with-a-specific-branch(-take-ev2-branch-as-an-example)
- c. Example for r17 integration
  - artifacts.merge
    https://dev.azure.com/E-OS/device/_git/artifacts.merge/commit/75dd09da831d00963ec8fce31951ad0ea0ae6d6d?refName=refs%2Fheads%2Fc1%2Fint%2F11%2Fr00017.0
  - artifacts.nhlos
    https://dev.azure.com/E-OS/device/_git/artifacts.nhlos/commit/47815a19befb9cbe23b4eeab01932fdc4dee2486?refName=refs%2Fheads%2Fc1%2F11%2Fmain
  - artifacts.vendor
    https://dev.azure.com/E-OS/device/_git/artifacts.vendor/commit/befbe384e48ed5618faa6722a2af20d8f58fd72e?refName=refs%2Fheads%2Fc1%2Fint%2F11%2Fr00017.0
- d. Replace c1-11-main-component to c1-int-11-component
- e. Replace qssi-11-main-component to qssi-int-11-component

## 13. Merge to SSI -> Done by William
- a. If vintf interface changed in new version, it need to modify for merge to ssi
  - https://dev.azure.com/DSQO-Taipei/Knowledge Share/_wiki/wikis/Knowledge-Share.wiki/85/Incompatible-VINTF-metadata-during-merge-ssi
  - https://dev.azure.com/E-OS/ssi/_git/device.surface.ssi/commit/1a2ed9d4d69eafc7d224b82128737cd215006f54?refName=refs%2Fheads%2Fssi%2F11%2Fmain

## 14. Int Artifacts:
- https://dev.azure.com/e-os/device/_packaging?_a=feed&feed=code-integration

## 15. Int Image:
- https://dev.azure.com/e-os/device/_packaging?_a=feed&feed=c1-int-11-images

## 16. Conflicts / Issues:
- a. Sensor: Ken Cheng -> Fixed
  - https://dev.azure.com/E-OS/Zeta/_workitems/edit/146540
- b. Cloud Signing Cert: Simon Tian -> Fixed
  - https://dev.azure.com/e-os/Zeta/_workitems/edit/146290
  - https://dev.azure.com/E-OS/device/_git/qcom-Lahaina.LA.1.0-premium-high-2020-spf-1-0_amss_standard_oem?path=%2Fcommon%2Fsectools%2Fresources%2Fdata_prov_assets%2FSigning%2FLocal%2Fms_prod_zeta_certs-key4096_exp65537_paddingPSS%2FMicrosoft_Surface_Duo_Attestation_Signer.cer&version=GC923ce1de6f085193b55c175d8064935613f17aa7
- c. Wifi: Jeff Lin -> Fixed
  - https://dev.azure.com/E-OS/Zeta/_workitems/edit/146710
- d. Charger, ADSP: Naomi French -> Fixed
  - https://dev.azure.com/E-OS/Zeta/_workitems/edit/146694
- e. Techpack Display: Sandeep Panda -> Un-Resolved
  - https://dev.azure.com/E-OS/Zeta/_workitems/edit/146287
- f. Prebuilt HY11: Nagappan Rathinam -> Fixed
  - https://dev.azure.com/E-OS/Zeta/_workitems/edit/146520
- g. Tiled Display: Dominik Rekawek (Sigma) -> Fixed
  - https://dev.azure.com/E-OS/Zeta/_workitems/edit/146304
- h. MPSS: Young Rang Do -> Fixed
  - https://dev.azure.com/E-OS/Zeta/_workitems/edit/146288
i. TZ.APPS: Ravindra Jain -> Fixed
  - https://dev.azure.com/E-OS/Zeta/_workitems/edit/147274

## 17. Local Build if Necessary
- https://dev.azure.com/e-os/device/_wiki/wikis/Wiki/34172/Building-C1-Zeta-on-Android-11

## 18. Workaround:
- a. Removed
  - (1). https://dev.azure.com/e-os/Zeta/_workitems/edit/146352
    - (a). In C8, Qcom try to covert display from built-in to module
    - (b). export CONFIG_DISPLAY_BUILD=m
    - (c). In this workaround, we change it back to built-in method.
  - (2). https://dev.azure.com/e-os/Zeta/_workitems/edit/146359
    - (a). Qcom assume display will be built into a module, 
    - (b). But we got some build error so we change it to built-in.
    - (c). consequently, we comment out these lines.
  - (3). https://dev.azure.com/e-os/Zeta/_workitems/edit/146365
    - (a). CONFIG_BUILD_TAG  =n
  - (4). https://dev.azure.com/e-os/Zeta/_workitems/edit/146695
    - (a). Enable ADSP restart by changing setprop persist.vendor.ssr.restart_level "adsp" in subsystem_restart_int.sh
- b. Remained
  - https://dev.azure.com/e-os/Zeta/_workitems/edit/146376
    - (a). For solving build error of display kernel module.
    - (b). CONFIG_DISPLAY_BUILD - keep this one and display team will solve it in main line.
    - (c). msm_drm.ko - keep this one and display team will solve it in main line.
    - (d). CONFIG_BUILD_TAG - already reverted.
    - (e). Adsp crash bug - already reverted.

## 19. Keep comparing the diffs of manifest between c1/11/main and c1/int/11/c8_00005.9
- a. In E-OS/device
  - (1). c1/11/main, c1/int/11/c8_00005.9
    - (a). Commit 9317ed41: use azcli.eos-11:lkg to support many users
  - (2). qssi/11/main, c1-qssi/int/11/c8_00005.9
- b. In E-OS/ssi
  - (1). ssi/11/main, ssi/int/11/c8_00005.9
    - (a). Commit 2221a1a7: Merged PR 23117: Update packages.surface.services.telephony-build-ssi-pr.yaml for Azure Pipelines
	
## 20. Find which cloud build for c1/11/main we are using:
- a. In Artifacts -> code-integration -> c1-mainfest xxxx
- b. In Description, it will show build id and version for ssi and qssi
- c. For Example: https://dev.azure.com/e-os/device/_packaging?_a=package&feed=code-integration&package=c1-manifest&protocolType=UPack&version=2021.413.1&view=overview

## 21 Release Candidate (RC): 2021.414.11
- a. Combo:
  - https://dev.azure.com/e-os/device/_packaging?_a=package&feed=c1-int-11-images%40Local&package=c1-11-developer-combo&protocolType=UPack&version=2021.414.11
- b.  EDL:
  - https://dev.azure.com/e-os/device/_packaging?_a=package&feed=c1-int-11-images%40Local&package=c1-11-developer-edl&protocolType=UPack&version=2021.414.11
- c. Based on c1/11/main cloud build, ssi: 2021.417.3 (buildid: 570270), qssi: 2021.417.2 (buildid: 576267)
- d. Without TZ.APPS Solution:
  - https://dev.azure.com/E-OS/Zeta/_workitems/edit/147274

## 22. Code Freeze (c1/11/main) -> Done by Neel (04/19/2021, 9am)

## 23. Archive:
- a. No changes in manifest for c1/11/main, qssi/11/main, and ssi/11/main
- b. create-repo-list: c1/11/main cloud build, ssi: 2021.417.3 (buildid: 576356), qssi: 2021.417.2 (buildid: 576267) -> int: 2021.418.1, https://dev.azure.com/e-os/device/_build/results?buildId=578421&view=artifacts&pathAsName=false&type=publishedArtifacts
- c. create-branch:
  - (1). Branch/tag: bsp/code-integration
  - (2). Is it archive: YES
  - (3). Feed Version: 2021.418.1 (create-repo-list result)
  - (4). New Branch Name: 11/r00020.2 (the last int name)
  - (5). Chech the result:
    - (a). https://dev.azure.com/e-os/device/_build/results?buildId=578424&view=artifacts&pathAsName=false&type=publishedArtifacts
    - (b). Published -> artifact-json ->  repos_modified.xlsx
- d. Archive for manifest manually
  - (1). c1/11/main -> archive/c1/11/r00020.2
  - (2). qssi/11/main -> archive/qssi/11/r00020.2
  - (3). ssi/11/main -> archive/ssi/11/r00020.2

## 24. Create the final image for c1/11/main
- a. run-pipeline-build
  - (1). Branch/tag: bsp/code-integration
  - (2). Manifest Branch: c1/11/main
  - (3). QSSI Manifest Branch: qssi/11/main
  - (4). SSI Manifest Branch: ssi/11/main

## 25. Final Diff:
- a. No changes in manifest for c1/11/main, qssi/11/main, and ssi/11/main
- b. create-repo-list:  
  - c1/11/main cloud build, ssi: 2021.417.3 (buildid: 576356), qssi: 2021.417.2 (buildid: 576267) -> int: 2021.418.1, https://dev.azure.com/e-os/device/_build/results?buildId=578421&view=artifacts&pathAsName=false&type=publishedArtifacts
- c. create-patch: last, Seed: 2021.414.1 Base: 2021.415.1 -> https://dev.azure.com/e-os/device/_packaging?_a=package&feed=code-integration&package=c1-patch&protocolType=UPack&version=2021.418.2
- d. apply-patch: 2021.418.1 -> https://dev.azure.com/e-os/device/_packaging?_a=package&feed=code-integration&package=c1-apply&protocolType=UPack&version=2021.418.1
- e. run-pipeline-build -> 2021.418.5
  - (1). Branch/tag: bsp/code-integration
  - (2). Manifest Branch: c1/int/11/c8_00005.9
  - (3). QSSI Manifest Branch: c1-qssi/int/11/c8_00005.9
  - (4). SSI Manifest Branch: ssi/int/11/c8_00005.9
    - Combo: https://dev.azure.com/E-OS/device/_packaging?_a=package&feed=c1-int-11-images%40Local&package=c1-11-developer-combo&protocolType=UPack&version=2021.418.5
    - EDL: https://dev.azure.com/E-OS/device/_packaging?_a=package&feed=c1-int-11-images%40Local&package=c1-11-developer-edl&protocolType=UPack&version=2021.418.5

## 26. Notify CICD that there are some ssi repo need to be push ssi/int/11/c8_00005.9 to ssi/11/main
  - caf-device.qcom.sepolicy - Repos (azure.com)
  - device.surface.ssi - Repos (azure.com)
  - priv-aosp-platform.frameworks.base - Repos (azure.com)
  - qcom-sm8350.qssi.11.proprietary.common - Repos (azure.com)
  - qcom-sm8350.qssi.11.proprietary.commonsys-intf.data - Repos (azure.com)
  - qcom-sm8350.qssi.11.proprietary.commonsys.diag - Repos (azure.com)
  - qcom-sm8350.qssi.11.proprietary.commonsys.display - Repos (azure.com)
  - qcom-sm8350.qssi.11.proprietary.commonsys.ims-ship - Repos (azure.com)
  - qcom-sm8350.qssi.11.proprietary.commonsys.qcrilOemHook - Repos (azure.com)
  - qcom-sm8350.qssi.11.proprietary.commonsys.qmi-framework - Repos (azure.com)
  - qcom-sm8350.qssi.11.proprietary.commonsys.telephony-fwk - Repos (azure.com)
  - qcom-sm8350.qssi.11.proprietary.commonsys.wfd - Repos (azure.com)
  - qcom-sm8350.qssi.11.proprietary.interfaces - Repos (azure.com)
  - qcom-sm8350.qssi.11.proprietary.prebuilt_HY11 - Repos (azure.com)

## 27. Int to Main -> Done by Neel (04/20/2021 15:30)

## 28. Check List:
- a. Auto Build:
  - (1). https://dev.azure.com/e-os/device/_git/manifest/commit/c838b42bc0b5d8efd6f0765dbf26ddec80dca0c5?refName=refs%2Fheads%2Fc1%2F11%2Fmain
  - (2). Change Scheduled Rolling Builds as TRUE
- b. UTF is OK: https://dev.azure.com/E-OS/device/_build/results?buildId=581106&view=ms.vss-test-web.build-test-results-tab
- c. Security Check: Booting succeeded on a fused device with the customer image

# Comparing with Hi2020 r00020.2 and c8_00005.9
## 0. Version Info
- a. For r00020.2
  - LA.QSSI.11.0.r1-09600-qssi.0-1
  - LA.UM.9.14.r1-12800-LAHAINA.0-1
  - LE.UM.4.3.1.r1-03200-genericarmv8-64.0-1
- b. For c8_00005.9
  - LA.QSSI.11.0.r1-11100-qssi.0-1
  - LA.UM.9.14.r1-15100-LAHAINA.0-1
  - LE.UM.4.3.1.r1-03700-genericarmv8-64.0-1
## 1. caf
- a. LE.UM.4.3.1
  - (0). About
    - (a). open embeded
    - (b). core-technologies.lnx.3.0.r10
    - (c). msm-5.4.r2
    - (d). yocto.lnx.3.1.r4
    - (e). display-le.lnx.1.0.r1
    - (f). sec-userspace.lnx-meta.6.1.r1
    - (g). le-sepolicy.lnx.3.0.r8
    - (h). le-blast.lnx.1.4.r4
    - (i). display.lnx.7.0.r2
    - (j). display-kernel.lnx.5.4.r2
    - (k). display-sysintf.lnx.1.2.r9
    - (l). le-frameworks.lnx.2.1.r4
  - (1). caf-private_le/external.* -> caf-ype/external.*
  - (2). caf-private_le/fs.external.mtd-utils -> caf-ype/quic.filesystem.fs.external.mtd-utils
  - (3). caf-private_le/kernel.build, msm-5..4 -> caf-ype/kernel.build, msm-5..4
  - (4). caf-private_le/meta-*, platform.* -> caf-ype/quic.le.meta-*, platform.*
  - (5). caf-private_le/qti-conf -> caf-ype/quic.le.qti-conf
- b. LA.UM.9.14
  - (0). About
    - uefi.lnx.2.1.r3-rel
    - qcom-devices.lnx.6.0.r3-rel
    - sepolicy.vndr.lnx.1.0.r6-rel
    - kernel.lnx.5.4.r1-rel
    - audio-hal.lnx.8.0.r4-rel
    - android-core.lnx.6.0.r3-rel
    - display.lnx.7.0.r1-rel
    - location.lnx.6.0.r2-rel
    - lnx.omx.core.1.0.r1-rel
    - ppat-corepower.lnx.1.0.r3-rel
    - wlan-aosp.lnx.6.0.r1-rel
    - camera-SnapdragonCamera.lnx.4.0.r3-rel
    - wlan-service.lnx.6.0.r1-rel
    - nfc.vendor.lnx.2.0.r2-rel
    - audio-driver.lnx.5.0.r1-rel
    - camera-kernel.lnx.4.0.r1-rel
    - data-kernel.lnx.1.1.r1-rel
    - display-kernel.lnx.5.4.r1-rel
    - video-kernel.lnx.1.0.r1-rel
    - data.lnx.6.0.r2-rel
    - wigig-vndr.lnx.6.0.r1-rel
    - core-technologies.lnx.3.0.r3-rel
    - power.lnx.3.0.r8-rel
    - opensource-tools.lnx.1.0.r99-rel
    - wlan-api.lnx.1.0.r65-rel
    - wlan-cmn.driver.lnx.2.0.r12-rel
    - wlan-cld3.driver.lnx.2.0.r11-rel
  - (1). LA.QSSI.11.0.r1, tag: AU_LINUX_ANDROID_LA.QSSI.11.0.R1.11.00.00.668.096 -> xxx.668.111.00
- c. LA.QSSI.11.0
  - (0). About
    - ks-aosp.lnx.3.0.r4-rel
    - ant-sysinf.lnx.1.0.r2-rel
    - android_ui-sys.lnx.5.0.r2-rel
    - atel-sys.lnx.1.0.r4-rel
    - nfc.intf.lnx.2.0.r3-rel
    - av-aosp-qc.lnx.11.0.r4-rel
    - bt.lnx.6.0.r4-rel
    - btcommon.lnx.6.0.r3-rel
    - android-core-sysinf.lnx.6.0.r3-rel
    - qcom-qssi.lnx.6.0.r2-rel
    - data-sys.lnx.6.0.r2-rel
    - display-sysinf.lnx.1.2.r3-rel
    - fm.lnx.6.0.r3-rel
    - android-vendor-hals.lnx.1.1.r53-rel
    - wfd-userspace-sysinf.lnx.5.0.r2-rel
  - (1). Remove OpenCL-CTS
## 2. hlos/vendor-core.xml
- a. LA.QSSI 09600 -> 11100
- b. LA.UM 12800 -> 15100 
## 3. nhlos/*.xml
- a. devoce/qcom-MPSS.HI.4.3 -> MPSS.HI.4.0 (have been done in main already)
## 4. nhlos/le.xm and nhlos.xml
- a. LE.UM 03200 -> 03700
## 5. projects/projects-nhlos-qcom.xml
- a. Cedros.LA.1.1 -> 1.0
- b. Lahaina.LA.1.1 -> 1.0
## 6. new yaml/cron/hi2020-crs-merge-cron.yaml
## 7. yaml/merge-build.yaml
- a. -name: buildSelfhos, default: true -> false
## 8. new yam/merge-crs-build.yaml and merge-crs-manifest.yaml
## 9. yam/tz.apps-build.yaml
- a. New buildJob: Build_Release_Cedros
## 10. remotes.xml
- a. eos_build: eos/11/main
- b. device-caf: hi2020/int/11/r00020.2 -> hi2020/int/11/c8_00005.9
- c. device-com: hi2020/int/11/r00020.2 -> hi2020/int/11/c8_00005.9
- d. device: hi2020/11/main
- e. device-int: hi2020/int/11/r00020.2 -> hi2020/int/11/c8_00005.9
- f. caf: partner-android/r-fs-release
- g. caf-qssi: partner-android/r-fs-release
- h. caf-le: refs/tags/LE.UM.4.3.1.r1-03100 (should be 03200) -> 03700
- i. qcom, qcom-qssi, qcom-le: refs/tags/r1.0.r1_00020.2 -> r1.0.c8_00005.9
- j. partner-aosp: r-fs-release

# Stuffs
## Schedule (PST):
- a. 3/29
- b. 4/5
  - (1). CICD done to move QC release into ADO repo
  - (2). Start to do code integration
- c. 4/6
- d. 4/7
- e. 4/8
- f. 4/9
- g. 4/12
- h. 4/13

## Original Manifest XML from Qcom: https://dev.azure.com/E-OS/device/_git/manifest?path=%2Fcaf%2FLA.UM.9.14.r1-15100-LAHAINA.0.ado.xml&version=GBhi2020%2Fint%2F11%2Fc8_00005.9
- 1. LA.QSSI.11.0.r1-11100-qssi.0.ado.xml
- 2. LA.UM.9.14.r1-15100-LAHAINA.0.ado.xml
- 3. LE.UM.4.3.1.r1-03700-genericarmv8-64.0.ado.xml

## Steps:
- 1 11th/March Release
  - a. 1.1 -> 1.0 CS
  - b. Compare
- 2. Integrate
- 3. 7350 Buildiable
  - a. XBL and ABL are the same
  - b. Most of NHLOS have different commends and repo on 7350

## Meeting Minutes:
- 1. 03/23/2021
  - a. CRS: Cornos HW Bring-Up
  - b. Caf / Private
  - c. Modem
  - d. Device Tree (Single Device Tree for Zeta and CRS) -> William
    - (1). DTBO -> 24MB
  - e. Subsystem to check with CRS
- 2. 03/30/2021
  - a. Use a task to track the changes Neel do after starting the code integration.
  - b. Use the same QSSI
  - c. One XBL repo with different target to build Laahaina and Cedros in makefile.main.mk
  - d. DV SMT 5/28/2021
  - e. 5/29
