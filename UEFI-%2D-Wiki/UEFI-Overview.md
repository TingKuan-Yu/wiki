# Useful Resuource
- ## Qualcomm Document
  - 80-P2484-37 K Linux Android UEFI Integration
  - 80-NA797-1 D Unified Extensible Firmware Interface (UEFI) Overview
  - 80-PK177-11 SM8350 Boot and CoreBSP Architecture Overview

- ## Tianocore
  TianoCore, the community supporting an open-source implementation of the Unified Extensible Firmware Interface (UEFI). This Foundation Code, developed by Intel as part of a project code named Tiano, was Intel’s “preferred implementation” of EFI. This evolved into EDK, EDK II, and other open source projects under the TianoCore community.
  - https://www.tianocore.org/
  - https://github.com/tianocore/tianocore.github.io/wiki/UEFI-EDKII-Learning-Dev
  - https://github.com/tianocore-training/Tianocore_Training_Contents/wiki
  - https://edk2-docs.gitbook.io/edk-ii-uefi-driver-writer-s-guide/

- ## Internal documents
  - https://dev.azure.com/E-OS/device/_wiki/wikis/Wiki/35366/UEFI-Dev-Guide
  - https://dev.azure.com/e-os/device/_wiki/wikis/Wiki/25634/SurfaceUEFI-Build-Commands

- ## Project MU
  - https://microsoft.github.io/mu/WhatAndWhy/overview/


# Overview

UEFI defines a software interface between an operating system (OS) and platform
firmware. The interface consists of data tables that contain platform-related information,
plus boot and runtime service calls that are available to the OS and its loader. Together,
these provide a standard environment for booting an OS and running preboot applications.

QTI uses TianocoreEDK2 implementation for the UEFI specification. It is an open-source implementation available at http://www.tianocore.org/edk2/. The EDK2 software is with BSD license.

# UEFI history
- ~1998 - UEFI was known as Intel Boot Initiative; later changed to EFI
- 2005 - Intel stopped development of EFI at specification revision 1.1.0 and contributed it to the UEFI forum
- 2007 - Specification revision 2.1 released by the UEFI forum
- 2014 to 2015 – Specification revision 2.3 added ARM binding; revision 2.4 added AARCH64 bindings
- 2011 - EDK2 is available on Qualcomm WP/WA platforms since MSM8660.

# Why UEFI?
- Boot from large disks over **2TB** with a GUID partition table (**GPT**)
- CPU-independent architecture
- CPU-independent drivers
- Flexible pre-OS environment
- Modular design(M)

|Items|Before UEF  | After UEF |
|--|--|--|
|SBL/XBL  | Individual drivers code |Common drivers code |
|LK(Android)  |Duplicated drivers code   | Share drivers code with XBL |
|Code Framework  |  Coupled by Qualcomm Style| Integrated as UEFI Framework |
| Code Maintenance |  Individual, Rep|Simple, One-time  |

