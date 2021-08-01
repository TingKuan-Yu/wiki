# Image Naming Conventions
https://dev.azure.com/E-OS/device/_wiki/wikis/Wiki/28952/Image-Naming-conventions
https://dev.azure.com/E-OS/device/_wiki/wikis/Wiki/28940/BSP-Integrations-and-Upcoming-updates


# Zeta

- **c1-11-main-images is for image download** 
https://dev.azure.com/E-OS/device/_packaging?_a=feed&feed=c1-11-main-images

- **c1-11-main-component is for symbol download**
https://dev.azure.com/e-os/device/_packaging?_a=feed&feed=c1-11-main-component%40Local

- **APR/13/2021 int build - 2021.412.12**
  - EDL
https://dev.azure.com/E-OS/device/_packaging?_a=package&feed=c1-int-11-images%40Local&package=c1-11-developer-edl&protocolType=UPack&version=2021.412.12
 
  - Combo
https://dev.azure.com/E-OS/device/_packaging?_a=package&feed=c1-int-11-images%40Local&package=c1-11-developer-combo&protocolType=UPack&version=2021.412.12&view=overview
  
  - selfhost is user build
  - merged is the target file for ota

- Note
  1. the symbol file information for ramdump parsing
    - https://dev.azure.com/DSQO-Taipei/Knowledge%20Share/_wiki/wikis/Knowledge-Share.wiki/138/Symbol-file-for-ramdump
  2. where to download symbol file
    - refer to information wiki of combo or selfhost build to download every symbol separately



# Epsilon
- **b1-10-main-images Link**
https://dev.azure.com/E-OS/device/_packaging?_a=feed&feed=b1-10-main-images%40Local

- **Example** 
**b1-10-selfhost-ota**
az artifacts universal download \
  --organization "https://dev.azure.com/E-OS/" \
  --feed "b1-10-main-images" \
  --name "b1-10-selfhost-ota" \
  --version "2021.412.1" \
  --path .
