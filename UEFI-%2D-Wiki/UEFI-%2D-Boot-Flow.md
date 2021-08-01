# SM8350 UEFI bootloader
- Source code of UEFI code exist in edk2 ( or called ABL) and boot_images.
  - 6. QHEE executes the XBL_CORE (or XBL region #), and then the XBL_CORE mounts and runs the unified extensible firmware interface (UEFI) application processor (ABL firmware volume(FV)).
  - 7. XBL core loads and authenticates encrypted SP (Secure Processor) main control program (MCP) images into DDR.
  - 8-8. UEFI peripheral image loader (PIL) driver brings the SP out of reset. The SP PBL decrypts SP MCP images, loads it noto SP SRAM and then authenticates and runs it.
  - 9. The Linux load application (part of ABL FV) loads and authenticates the HLOS kernel with verified boot.
![sm8350bootflow.png](/.attachments/sm8350bootflow-979a989a-b2c4-4892-af9b-6356e3906176.png)


# UEFI bootl flow from Tianocore
Tht TianoCore is designed to implement the UEFI and UEFI PI (Platform Initialization) specifications.
![xts.png](/.attachments/xts-8a44e9cb-53fa-4fc4-b1ba-44d8f08d10f3.png)