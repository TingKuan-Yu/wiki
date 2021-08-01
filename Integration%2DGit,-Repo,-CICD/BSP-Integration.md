[[_TOC_]]


# Training

## Introduction to Surface System Image, Android builds in 2021
https://msit.microsoftstream.com/video/0623a1ff-0400-a605-b7e3-f1eb5048c0f2?referrer=https:%2F%2Fonenote.officeapps.live.com%2F

## Live Session - BSP ingestion and Flashing QRD using base QC drop
  - https://dev.azure.com/E-OS/device/_wiki/wikis/Wiki/95199/Live-Sessions
    - PPT: https://dev.azure.com/E-OS/ce81bee4-8e73-47a6-9208-5f2cee8eb4d7/_apis/git/repositories/cd9c4d86-a2e9-49ec-9765-8fd57f95b033/Items?path=%2F.attachments%2FBSP-Ingestion-8b7c0581-207b-4cba-9124-ef8e739e27a8.pptx&download=false&resolveLfs=true&%24format=octetStream&api-version=5.0-preview.1&sanitize=true&versionDescriptor.version=master
   - Video: https://msit.microsoftstream.com/video/1825a4ff-0400-94b1-fb51-f1eb9283532a

# Introduction
- 1. Get new code base from aosp/qcom/caf public&private/Qualcomm Chipcode
- 2. CICD creates buildable branch
- 3. Adjust repository according to CICD code base
- 4. Apply Microsoft patches on item 3.
  - need to fix merge conflict
- 5. Make sure new sources are buildable
- 6. Make sure the new image could run well on device
- 7. Pass Q's test
- 8. Archive the main branch and then overwrite integration branch back to main
- 9. Apply some new main patches during integration.



