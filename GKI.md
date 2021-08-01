# Documents
- https://www.kernel.org/doc/Documentation/kbuild/modules.txt
- https://android.googlesource.com/kernel/build/+/refs/heads/master/abi/README.md



# Task
- https://dev.azure.com/E-OS/Zeta/_workitems/edit/136033
 - [GMS] DUT stuck rebooting after flashing GKI image for Cts-on-GSI and VTS testing


# Merged PRs

## Task 171871: GKI Booting: Add necessary modules to vendor_boot
- https://dev.azure.com/E-OS/Zeta/_workitems/edit/171871
- Pull Request 26999: Loading vendor ramdisk modules from kernel.json 
  - https://dev.azure.com/E-OS/device/_git/8f6ab1a7-d160-460d-a8c2-8b62fe505475/pullrequest/26999?_a=commits
    - E-OS/device/Repos/Commits/device.config

## Task 171872: GKI Booting: Adjust the module loading seqenece to fix unbootable issue
- https://dev.azure.com/E-OS/Zeta/_workitems/edit/171872
- Pull Request 26695: generate modules.load file from VENDOR_RAMDISK_KERNEL_MODULES
  - https://dev.azure.com/E-OS/device/_git/caf-kernel.build/pullrequest/26695?_a=overview
    - E-OS/device/Repos/Commits/caf-kernel.build

- Pull Request 26998: use predefined modules.load for vendor-ramdisk
  - https://dev.azure.com/E-OS/device/_git/device.oemc1.oemc1/pullrequest/26998?_a=overview
    - E-OS/device/Repos/Commits/device.oemc1.oemc1

## Task 171868: GKI Booting: Fix disagrees about version of symbol module_layout
- https://dev.azure.com/E-OS/Zeta/_workitems/edit/171868/
- Pull Request 26578: GKI Booting: fix disagress about version of symbol module_layout
  - https://dev.azure.com/E-OS/device/_git/caf-kernel.msm-5..4/pullrequest/26578?_a=overview
    - E-OS/device/Repos/Commits/caf-kernel.msm-5..4

## Task 171869: GKI Booting: Modulizing the module which GKI needs.
- https://dev.azure.com/E-OS/Zeta/_workitems/edit/171869
- Pull Request 27005: Make surface libraries as modules for GKI build
  - https://dev.azure.com/E-OS/device/_git/caf-kernel.msm-5..4/pullrequest/27005?_a=overview
  - E-OS/device/Repos/Pull requests/caf-kernel.msm-5..4

