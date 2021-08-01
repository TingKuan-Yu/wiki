[[_TOC_]]

# 1. log in devops
- az login
- az devops login
  - now, paste token
	  
# 2. pull abl source
- repo init
```
tony@UbuntM-VB:~/Zeta/c1_11_main/abl_checkin$ repo init -u ssh://ssh.dev.azure.com/v3/e-os/device/manifest -b c1/11/main -m nhlos/abl.xml
Downloading Repo source from https://gerrit.googlesource.com/git-repo
remote: Counting objects: 7, done
remote: Finding sources: 100% (136/136)
Receiving objects: 100% (136/136), 146.69 KiB | 314.00 KiB/s, done.
remote: Total 136 (delta 73), reused 134 (delta 73)
Resolving deltas: 100% (73/73), completed with 25 local objects.
Downloading manifest from ssh://ssh.dev.azure.com/v3/e-os/device/manifest
remote: Azure Repos
remote: Found 19963 objects to send. (564 ms)

Your identity is: Tony Yu <tingkuanyu@microsoft.com>
If you want to change this, please re-run 'repo init' with --config-name

repo has been initialized in /home/tony/Zeta/c1_11_main/abl_checkin
```
- repo sync
```
tony@UbuntM-VB:~/Zeta/c1_11_main/abl_checkin$ repo sync -j 2

device/qcom-Lahaina.LA.1.0-premium-high-2020-spf-1-0_amss_standard_oem:
fatal: Could not read from remote repository.

Please make sure you have the correct access rights
and the repository exists.

Fetching: 14% [2 jobs] (1/7) started eos/buildConnection to ssh.dev.azure.com closed by remote host.
Fetching: 100% (7/7), done in 8m14.131s
Checking out files: 100% (4830/4830), done.
Checking out files: 100% (13805/13805), done.
Checking out: 100% (7/7), done in 4.386s
repo sync has finished successfully.

tony@UbuntM-VB:~/Zeta/c1_11_main/abl_checkin$ ls
about.html  artifactcopy.py  artifacts  bootable  BOOT.MXF.1.0  build.sh  eos_build  Lahaina.LA.1.0  Makefile  root  scripts
```

# 3. create branch for develop
```
tony@UbuntM-VB:~/Zeta/c1_11_main/abl_checkin/bootable/bootloader/edk2$ git branch
* (no branch)
tony@UbuntM-VB:~/Zeta/c1_11_main/abl_checkin/bootable/bootloader/edk2$ repo start soc_serial_dev .
tony@UbuntM-VB:~/Zeta/c1_11_main/abl_checkin/bootable/bootloader/edk2$ repo sync -c .
Fetching: 100% (1/1), done in 4.821s
Connection to ssh.dev.azure.com closed by remote host.
repo sync has finished successfully.

tony@UbuntM-VB:~/Zeta/c1_11_main/abl_checkin/bootable/bootloader/edk2$ repo branch
*  soc_serial_dev            | in bootable/bootloader/edk2
```
# 4. apply branch
```
tony@UbuntM-VB:~/Zeta/c1_11_main/abl_checkin/bootable/bootloader/edk2$ git am ~/Zeta/c1_11_main/0001-c1_11-abl-support-fastboot-oem-get-soc-serial-comman.patch
Applying: c1_11: abl: support 'fastboot oem get-soc-serial' command to get SOC serial number
.git/rebase-apply/patch:44: trailing whitespace.
    if ((Status = pChipInfoProtocol->GetSerialNumber(pChipInfoProtocol, 
.git/rebase-apply/patch:55: trailing whitespace.
    FastbootInfo (SerialNumInfo);  
warning: 2 lines add whitespace errors.
```
# 5. push change to remote
```
tony@UbuntM-VB:~/Zeta/c1_11_main/abl_checkin/bootable/bootloader/edk2$ git push device-caf soc_serial_dev
Counting objects: 8, done.
Compressing objects: 100% (7/7), done.
Writing objects: 100% (8/8), 1.08 KiB | 28.00 KiB/s, done.
Total 8 (delta 7), reused 1 (delta 1)
remote: Analyzing objects... (8/8) (252 ms)
remote: Checking for credentials and other secrets... (3/3) done (148 ms)
remote: Storing packfile... done (76 ms)
remote: Storing index... done (51 ms)
To ssh://ssh.dev.azure.com/v3/e-os/device/caf-abl.tianocore.edk2
 * [new branch]            soc_serial_dev -> soc_serial_dev
```
# 6. create pull request
- Now, We can use devops to create draft pull request.
  - https://dev.azure.com/E-OS/device/_git/caf-abl.tianocore.edk2/pullrequest/23727
