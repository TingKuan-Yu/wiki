# device Terminology.md
https://dev.azure.com/E-OS/device/_git/wiki?path=%2FTerminology.md&_a=contents&version=GBmaster

Additional Terms at: [Image - Naming conventions](https://dev.azure.com/E-OS/device/_wiki/wikis/Wiki/3723/Image-Naming-conventions)

**3rdpty image** - for “outside” folks we need to give a build to. Most of the Surface/Microsoft apps removed. A shareable reference.

**ABL** - Android Bootloader. Runs as an XBL/UEFI app.

**ABS** ABnormal Shutdown
  - https://www.deviceswiki.com/wiki/Abnormal_shutdown 

**ACR** - Azure Container Registry

**ADB** - Android Debug Bridge. Devices Test server/tool.

**ADBD** - ADB Deamon

**ADSP** - Audio DSP

**ANR** - Activity/Application Not Responding

**apis** - API's - Application Programming Interface

**APK** - Android Package Kit (APK for short) is the package file format used by the Android operating system for distribution and installation of mobile apps. Just like Windows (PC) systems use an .exe file for installing software, the APK does the same for Android.

**aosp** - AOSP - Android Open Source Project, core codebase for Android

**AOP** - Aspect-Oriented Programming) framework for Android app development, based on the work of open-source Xposed framework project. 

**ATT** - AT&T cellular provider company

**att image** - for AT&T, with their unique additions

**BIH** Bits in Hand (PQ BIH). A [Surface SW Milestone](https://deviceswiki.com/wiki/Software_Milestone_Definitions).

**BITS** – Basic Integration Test Suite. Several tests are run before integrating. (And see Smoke test)

**Box Build** - Device in target enclosure. A box build includes all the other assembly work involved in an electromechanical assembly.

**BSP** - Board Support Package.  Software that implements and supports an operating system and device drivers on a particular standard development board. Typically includes a boot loader, an original equipment manufacturer adaptation layer, device drivers, and a default hardware component list.

**BSP branch** – contains releases from qualcomm and cookie updates

**BTS** - a) Back To School. Refers to customer release in spring or summer.
          b) Build To Stock. Build ahead approach.

**Build (verb)** - Construction of an artifact

**Build artifact_** - Output from a build

**Build/boot test** - Test for quickly verifying basic functionality (device/subsystem alive)

**CAF** - [Code Aurora Forum](https://www.codeaurora.org/) Qualcomm's open source Android repository. And we use as QC private branches (8.1)

**CDSP** - Compute DSP

**[CICD Naming conventions](https://dev.azure.com/e-os/device/_wiki/wikis/Wiki/17327/Build-and-LKG-Release-Naming-Conventions)**

**CHID** - Computer Hardware Identification. [Microsoft info](https://docs.microsoft.com/en-us/windows-hardware/drivers/install/specifying-hardware-ids-for-a-computer). [WikiHow.com](https://www.wikihow.com/Find-Hardware-ID)

**CLOG** - Candidate LKG OTA Google

**CTS** - [Compatibility Test Suite](https://source.android.com/compatibility/cts). A device is required to pass this to be branded an Android compatible device by Google.

**customer image** - the build targeting what is installed on an end device.

**Cuttlefish** - a build of Android that will run on x86 HW directly but specifically tuned for a VM. Behaves 'exactly' like a device as opposed to the current (Goldfish) emulator.

**DCR** - Design Change Request. Used to indicate a need to reevaluate feature decisions.

**Deploy** - Make a release artifact available externally

**DTBO** - Device Tree Binary Object; the compiled device tree.

**EXR** Experience Review or End to End Experience Review 

**FAI** - First Article Inspection performed on an initial sample of a product

**FDR** - Factory Data Reset

**Feed** - Package Feeds provide a directory of packages that can be installed.

**FFBM** - Fast Factory Boot Mode

**FFW** - Final Flash Firmware

**FPP** - Full Packaged Product

**FRP** - Factory Reset Protection

**Fusing** - Refers to manufacturing step after load/config of code, data where fuses are burned in the device to prevent access to specific memory.

**GEN** - Generic - Open Market image for Surface Duo

**GMS** - Google Mobile Services. Suite of Google-branded apps and services developed and owned by 
Google. Applications include Chrome, Gmail, Google Play, Drive, Maps, YouTube, etc.

**GOMA** - Code codename for Google distributed system; (internally will be placed on Azure)

**GOTA** - Google OTA

**GSI** - Google System Image

**GTS** - Google Mobile Services Test Suite

**HLOS** - High Level Operating System (Android)

[**Hardware Terminology**](https://deviceswiki.com/wiki/FAI_FPP_and_SKU_Build_Management#Acronyms)

**HWC** - Hardware Composer

**IFW** - Intermediate Flash Firmware

**image "3rdpty"** - for “outside” folks we need to give a build to. Most of the Surface/Microsoft apps removed. A shareable reference.

**image "combo"** - ___

**image "Customer"** - customer

**image "GEN"** - DEV build (LKG Images)

**image "mergezip"** - ___

**image "SFCL"** - Software For Certification Labs

**image "SH"** - SelfHost (Customer images with logging for SH program)

**image "version"** - ___

**image "edl"** - ___

**JSON** - JavaScript Object Notation

**JWT** - JSON Web Token, see jwt.io To securely transmit info between parties as a JSON object.

**LE** - Lab Entry; e.g. Lab Entry (LE) Drop, ATT would get `LE Drop -> IFW -> FFW`

**LKG** - Last Known Good

**LUN** - Logical Unit Numbers. The storage unit on the device will be separated into multiple LUN’s.

**Manifest** - Describes where source code for several gits can be fetched and where to store it locally [see format (XML)](https://gerrit.googlesource.com/git-repo/+/master/docs/manifest-format.md)

**MCU** - Micro Computer Unit

**MTP** - Modem Test Platform ( Qualcomm Reference Phone Design for OEMs  )


**nHLOS** - non High Level OS. Qualcomm(?) lingo for all the parts that are not the HLOS, for example Bootloader, Modem software, etc...

**Nightly build (pipeline)** - Scheduled pipeline for building of release artifact and quality assurance of the same

**NuGet** - Tool for Packaging

**ODM** - Original Design Manufacturer (may be a bit 'used for other purposes' within builds)

**OTA** - Over the Air

[**Packaging**](https://deviceswiki.com/wiki/Packaging) - Use of binary packages (tools, libraries, etc.) as dependencies. This allows greater reuse across products and no repo bloat.

**Package Feed** - ____? (example b1-10-master-images)

**PAI** - Playstore Auto Install

**Pipeline** - Sequence of steps to ensure the construction and quality of an artifact

**PQ BIH** - Product Quality Bits In Hand. A [Surface SW Milestone](https://deviceswiki.com/wiki/Software_Milestone_Definitions).

**PR** - Pull Request. you make a patch w/ changes people can review, then make a build

**Pull request** - Activity to request integration of a work item to a maintained branch

**Pull request pipeline** - Pipeline run at a pull request

**Provisioning** - ____

**QCN** - Qualcomm Calibration N (Modem Calibration). Generally device unique, but Golden QCN's can be applied at times during development .

**QRD** - Qualcomm Reference Design

**RCA** - Root Cause Analysis

**Release artifact** - A stored, versioned and traceable artifact

**Release/Publish (verb)** - Make a build artifact available internally

**Repos** - Repository. Files for SW source code (src), test, etc.

**RTM** - [Release To Manufacturing](https://en.wikipedia.org/wiki/Software_release_life_cycle#Release_to_manufacturing_(RTM)) - when a software product is ready to be delivered

**SelfHost** - Image for SelfHosters

**[Semantic versioning](https://semver.org/)** – incremental versioning in tags where x.y.z stands for major.minor.patch upgrade

**SFPD** - SW Factory Program Data The SFPD partition will be our primary partition used to store factory related data that will be locked from editing outside of the factor.

**SFU** - Surface Feature Update, a frequently released LKG starting about RTM timeframe.

**SFU0** - SW Factory Update #0, after the RTM (to start the manufacturing), this is the first update of SW delivered to Factory to enable integration of new features and tools.

**SHA1** - Secure Hash Algorithm 1

**SHA1 Manifest** - List of increments included in a build. 

**SIG** - Share Image gallery

**SKU** - Stock Keeping Unit. A part number for a sellable item. Different configurations each have a SKU number.

**SFCL** - Software For Certification Labs

**slpi** - Sensors Low-Power Interface firmware for SPX

**Smoke test** - Checks after integration that SW still builds and boots up. (And see BITS)

**spss** - ___ code from Qualcomm

**SSI** - Surface System Image

**SUW** - Setup Wizard

[SW Milestone Definitions](https://deviceswiki.com/wiki/Software_Milestone_Definitions)

**TGL** - 

**ToT** - Tip of Tree

**UEFI** - Unified Extensible FW Interface. UEFI replaces BIOS.

**vmss** - Virtual Machine Scale Set 

**VTS** - [Vendor Test Suite](https://source.android.com/compatibility/vts) - introduced post-Android O, as part of Treble initiative, HIDL

**WLC** - Wireless Charging

**WVD** - [Windows Virtual Desktop](https://dev.azure.com/E-OS/epsilon/_wiki/wikis/Epsilon.wiki/25400/Windows-Virtual-Desktop-(WVD))

**xTS Automation** - ___(test automantion)

**YPC** - [Your Phone Companion API's](https://www.microsoft.com/en-us/p/Your-phone/9nmpj99vjbwv?activetab=pivot:overviewtab)

