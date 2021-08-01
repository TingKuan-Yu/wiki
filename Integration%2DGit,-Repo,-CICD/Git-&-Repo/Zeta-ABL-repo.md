[[_TOC_]]


# abl repo url
 - https://dev.azure.com/E-OS/device/_git/caf-abl.tianocore.edk2
 - Main branch is "c1/11/main"

# abl repo introduction
- Repo Groups
  - Repo is the tool that we use to manage our local checkouts. It parses the manifest specified by the default.xml file. The name of the manifest can be overridden using **-m**. **One could also check out a subset of the manifest using the repo groups feature.** 
  - Chromium OS repo manifest (for `repo init`): https://chromium.googlesource.com/chromiumos/manifest.git
- repo Element-remote
  - https://gerrit.googlesource.com/git-repo/+/HEAD/docs/manifest-format.md#Element-remote
  - example
```
.repo/manifests/projects/projects-nhlos-device.xml
<project remote="device-caf" groups="eos,build-abl,device-caf" name="device/caf-abl.tianocore.edk2" path="bootable/bootloader/edk2"/>
  ```
```
tony@tony-ST50:/android/zeta/c1/11/abl/bootable/bootloader/edk2$ cat .git/config 
[core]
	repositoryformatversion = 0
	filemode = true
[filter "lfs"]
	smudge = git-lfs smudge --skip -- %f
	process = git-lfs filter-process --skip
[remote "device-caf"]
	url = ssh://ssh.dev.azure.com/v3/e-os/device/caf-abl.tianocore.edk2
	projectname = device/caf-abl.tianocore.edk2
	fetch = +refs/heads/*:refs/remotes/device-caf/*
[branch "abl_neo_test"]
	remote = device-caf
	merge = refs/heads/c1/11/main
```
