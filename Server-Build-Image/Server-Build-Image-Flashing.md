# Setup for flashing
- https://dev.azure.com/E-OS/device/_wiki/wikis/Wiki/13/Setup-for-flashing


# Flashing
- https://dev.azure.com/E-OS/device/_wiki/wikis/Wiki/2193/Flashing

# Zeta: Image Flashing
- Windows/Ubuntu CLI installation; login ; Image Download
https://dev.azure.com/E-OS/device/_wiki/wikis/Wiki/13/Setup-for-flashing

- Zeta Board Setup and Image Flashing
https://dev.azure.com/E-OS/device/_wiki/wikis/Wiki/2193/Flashing

# LKG Flashing Guide
   - Last known good (LKG)
   - https://dev.azure.com/E-OS/device/_wiki/wikis/Wiki/25635/LKG-Flashing-Guide
   - For a brand new board
     - 1. Run **prov_ufs.cmd** from EDL package zeta_prov_ufs.jpg
Device will reset and host will continue see QDLoader again from host. 
       - not necessary for each time
     - 2. Run **edl_flash_bl.cmd** from EDL package.
     - 3. flash_reprovision.cmd for updating partition table
       - not necessary for each time
     - 4. flash.cmd for image update
