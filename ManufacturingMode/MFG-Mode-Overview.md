[[_TOC_]]
# Manufacturing Mode ( by Ken Hiatt )
  - https://dev.azure.com/e-os/device/_wiki/wikis/Wiki/25636/Manufacturing-Mode
    - describe method to enable or disable manufacturing mode
    - method to check manufacturing mode
# How-to-change-Surface-Duo-Manufacture-mode-state ( )
https://dev.azure.com/DSQO-Taipei/Knowledge%20Share/_wiki/wikis/Knowledge-Share.wiki/35/How-to-change-Surface-Duo-Manufacture-mode-state

# Linux AutoSign Tool
- https://www.deviceswiki.com/wiki/Signing_with_AutoSign
- Download tool for Linux
  - https://dev.azure.com/E-OS/tools/_packaging?_a=package&feed=linux-tools%40Local&package=autosignconsole&version=2.0.1&protocolType=UPack
- Download tool for Windows
  - https://dev.azure.com/MSFTDEVICES/Shared/_packaging?_a=package&feed=SurfacePackages&package=Devices.Tool.AutoSignConsole&version=1.5.129&protocolType=NuGet&view=overview
- Download source for Windows
  - https://dev.azure.com/MSFTDEVICES/Vulcan/_git/SurfaceDevCenterScripts
- Quick Notes
  - Web Auto Sign
    - refer to Signing_with_AutoSign wiki
    - http://autosign/request/


# Manufacturing Mode Overview
  - **Abstract**: (boot_images/boot/Sm8350FamilyPkg/Drivers/MsManufacturingModeDxe/MsManufacturingMode.c)
    This module looks to see if a NV-RAM variable exists.
    (ManufacturingModeSignatureVariableName).
    This blob (if set) is a PKCS7 formatted signature blob
    of the serial number of this device plus salt.  This blob is
    signed with a firmware servicing leaf signer of
    the Product Key certificate.

    If the signature is valid, and the leaf signer chains up
    to our Product Key, then we allow the firmware to go into
    Manufacturing mode.

    If the ManufacturingModeVariableName is not present,
    or it's size is 1, then we go into retail (Customer) mode,
    with manufacturing features disabled.

  - XBL key word: MsManufacturingMode
