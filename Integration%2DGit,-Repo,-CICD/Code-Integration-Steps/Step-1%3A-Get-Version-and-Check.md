
# Get integration version
- Get the version which you need to do code integration from SW PM

# Pre-check before integration
- Check with subsystem about binary file first for avoiding block code integration process.
  - we are using email to check with the subsystem about which version they prefer to use now.
  - Preferred version check table (Saved in William's OneDrive)
    - https://microsoft-my.sharepoint.com/:x:/p/fangruwu/EYBwnapBqa5BuQbPQpxC8GIBcNo4_jHsziaMK4Fo3UEKKQ?e=sLAHCG 
  - Check if CICD already complete the manifest and build for QC release code.
    - if you need to create manifest for QC release by yourself, it need to create caf xml
https://dev.azure.com/DSQO-Taipei/Knowledge Share/_wiki/wikis/Knowledge-Share.wiki/94/Create-caf-xml-from-QC-release
    - Note: CICD shall prepared a repo. However, it is worth to have a private test for fun.
  -

# Add a code integration status sub page 
  - under here
    - https://dev.azure.com/DSQO-Taipei/Knowledge%20Share/_wiki/wikis/Knowledge-Share.wiki/100/Code-Integration-version
  - sub page example: 
    - https://dev.azure.com/DSQO-Taipei/Knowledge%20Share/_wiki/wikis/Knowledge-Share.wiki/125/c8_00005.9
  - Content of sub page
    - Code base version information including their tags if it has.
    - Method to download integration source code
      - Vendor
      - Kernel
      - NHLOS
      - System QSSI ( Qualcomm Single System Image )
      - System SSI ( Surface System Image )
      - Merge
   - A excel file to record status for all patches
   - Integration issue status
   - Workaround for integration
   - RC ( Release Candidate) status
     - @TODO: Need to check with Bert or Amy
     - Apply patches from main during the integration period?
   - Archive Status
   - Other status
     - Auto Build Status
     - UTF Status
     - Booting status including on Fused device
   - Information about service build


# reference:
- Code integration (Amy Tang)
  - https://dev.azure.com/DSQO-Taipei/Knowledge%20Share/_wiki/wikis/Knowledge-Share.wiki/83/Code-integration