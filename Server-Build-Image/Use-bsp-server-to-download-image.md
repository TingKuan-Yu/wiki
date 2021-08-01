1. ssh to bsp server
- follow below wiki
https://microsoft-my.sharepoint.com/personal/yuyichen_microsoft_com/_layouts/15/Doc.aspx?sourcedoc={531bf1ca-f3d4-4825-b5d5-4f21fb08a988}&action=edit&wd=target%28BSP%20Lab.one%7C8a11d299-ab4b-4275-a429-a92b8b4c09ce%2FBuild%20Server%7C15e8f3a9-571b-4058-a897-c85075be8c16%2F%29
```
ssh bsp@172.23.114.97 
Account: bsp 
Password: P$5 
```

2. export PAT
```
bsp@bsp-build-serv:/media/bsp/disk2/Tony/images/develop_combo/2021.718.21$ export AZURE_DEVOPS_EXT_PAT=jjodvbknoy3oygjz4xwytd66xxf3ketpzgzhqiqy6adz2ks7rkdq
``

3. use az to download image
``
bsp@bsp-build-serv:/media/bsp/disk2/Tony/images/develop_combo/2021.718.21$ az artifacts universal download --organization "https://dev.azure.com/E-OS/" --feed "c1-11-main-images" --name "c1-11-developer-combo" --version "2021.718.21" --path .
 - Downloading ..
``

4. use filezila to download image