# Open manifest webiste to create a new branch
- web site - https://dev.azure.com/E-OS/device/_git/manifest/branches
- example create personal/tony/manifest/c1_11_abl_sign

![manifest.jpg](/.attachments/manifest-445fed9b-e4f1-4e28-b689-42cb1fd4ce85.jpg)
- **The pipeline yam branch also follows the new manifest branch.**
  - https://dev.azure.com/E-OS/device/_apps/hub/ms.vss-build-web.ci-designer-hub?pipelineId=1895&branch=personal%2Ftony%2Fmanifest%2Fc1_11_abl_sign
- we can also use this branch to sign other nonhlos images such as XBL.

# clone manifest for sign branch modification
```
tingkuanyu@TonyYuLinux1:/D/c1/11/main/manifest_nohlos$ git clone git@ssh.dev.azure.com:v3/E-OS/device/manifest -b personal/tony/manifest/c1_11_abl_sign manifest_ablsign
Cloning into 'manifest_ablsign'...
remote: Azure Repos
remote: Found 22749 objects to send. (938 ms)
Receiving objects: 100% (22749/22749), 6.07 MiB | 192.00 KiB/s, done.
Resolving deltas: 100% (14628/14628), done.
tingkuanyu@TonyYuLinux1:/D/c1/11/main/manifest_nohlos$ ls
manifest_ablsign
```

# prepare an abl personal branch for build and sign
- example: personal/tony/11/device_config
  - https://dev.azure.com/E-OS/device/_git/caf-abl.tianocore.edk2?version=GBpersonal%2Ftony%2F11%2Fdevice_config

# Add persional abl branch to manifest 

- add revision="personal/tony/11/device_config" to projects/projects-nhlos-device.xml
  <project remote="device-caf" groups="eos,build-abl,device-caf" name="device/caf-abl.tianocore.edk2" path="bootable/bootloader/edk2" revision="personal/tony/11/device_config" />

- commit 
```
tingkuanyu@TonyYuLinux1:/D/c1/11/main/manifest_nohlos/manifest_ablsign$ git status
On branch personal/tony/manifest/c1_11_abl_sign
Your branch is up to date with 'origin/personal/tony/manifest/c1_11_abl_sign'.

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
	modified:   projects/projects-nhlos-device.xml

no changes added to commit (use "git add" and/or "git commit -a")
tingkuanyu@TonyYuLinux1:/D/c1/11/main/manifest_nohlos/manifest_ablsign$ git add .
tingkuanyu@TonyYuLinux1:/D/c1/11/main/manifest_nohlos/manifest_ablsign$ git commit -m "add persional revision to abl"
tingkuanyu@TonyYuLinux1:/D/c1/11/main/manifest_nohlos/manifest_ablsign$ git push origin personal/tony/manifest/c1_11_abl_sign
```

- check website
  - https://dev.azure.com/E-OS/device/_git/manifest/commit/e321ce788456a390017e7f59c9594d8a3ad75ef9?refName=refs%2Fheads%2Fpersonal%2Ftony%2Fmanifest%2Fc1_11_abl_sign
```
<!-- Move ABL to NHLOS -->
Minus    <project remote="device-caf" groups="eos,build-abl,device-caf" name="device/caf-abl.tianocore.edk2" path="bootable/bootloader/edk2"/>
Plus    <project remote="device-caf" groups="eos,build-abl,device-caf" name="device/caf-abl.tianocore.edk2" path="bootable/bootloader/edk2" revision="personal/tony/11/device_config" />
```
# run pipeline to build and sign abl
- https://dev.azure.com/E-OS/device/_build?definitionId=1896&view=runs
- build abl: **E-OS/device/Pipelines/c1/11.0/manifest/build/nhlos/c1-11-abl-build**
  - Select manifest branch personal/tony/manifest/c1_11_abl_sign to run
![Screenshot at 2021-07-18 17-10-28.png](/.attachments/Screenshot%20at%202021-07-18%2017-10-28-ead425b1-aec2-4574-b29a-158971949e38.png)

- build manifest (just test, no use):  **E-OS/device/Pipelines/c1/11.0/manifest/c1-11-abl-manifest**
  - Select manifest branch personal/tony/manifest/c1_11_abl_sign to run
![Screenshot at 2021-07-18 16-52-16.png](/.attachments/Screenshot%20at%202021-07-18%2016-52-16-a871541e-8b0a-42e7-bb8f-c49867fbe0b6.png)