[[_TOC_]]


# repo test
```
tony@tony-ST50:/android/zeta/c1/11/abl/bootable/bootloader/edk2$ repo sync -c .

... A new version of repo (2.12) is available.
... You should upgrade soon:
    cp /android/zeta/c1/11/abl/.repo/repo/repo /home/tony/bin/repo

Connection to ssh.dev.azure.com closed by remote host.
Fetching: 100% (1/1), done in 6.208s
repo sync has finished successfully.
```

# git test
## git remote show
  -  show branches, push and pull url
```
tony@tony-ST50:/android/zeta/c1/11/abl/bootable/bootloader/edk2$ git remote show device-caf | more
* 遠端 device-caf
  取得位址：ssh://ssh.dev.azure.com/v3/e-os/device/caf-abl.tianocore.edk2
  推送位址：ssh://ssh.dev.azure.com/v3/e-os/device/caf-abl.tianocore.edk2
  HEAD 分支：c1/11/main
  遠端分支：
    LA.AU.0.0.1_rb1.22                                      已追蹤
    :

tony@tony-ST50:/android/zeta/c1/11/abl/bootable/bootloader/edk2$ git remote show device-caf | grep neo
    abl_neo_test                                            已追蹤
```
##git pull
- git pull is the combination of git fetch and git merge
```
tony@tony-ST50:/android/zeta/c1/11/abl/bootable/bootloader/edk2$ git pull device-caf c1/11/main
來自 ssh://ssh.dev.azure.com/v3/e-os/device/caf-abl.tianocore.edk2
 * branch                  c1/11/main -> FETCH_HEAD
已經是最新的。

tony@tony-ST50:/android/zeta/c1/11/abl/bootable/bootloader/edk2$ git pull device-caf abl_neo_test 
來自 ssh://ssh.dev.azure.com/v3/e-os/device/caf-abl.tianocore.edk2
 * branch                  abl_neo_test -> FETCH_HEAD
Merge made by the 'recursive' strategy.
 QcomModulePkg/Library/FastbootLib/FastbootCmds.c | 2 ++
 1 file changed, 2 insertions(+)

tony@tony-ST50:/android/zeta/c1/11/abl/bootable/bootloader/edk2$ git log -1
commit 98ccfc11221a1711304a350b473620de64b668ae (HEAD -> abl_neo_test)
Merge: eb3a61179e 797c5e1c02
Author: TingKuan Yu <tingkuanyu@microsoft.com>
Date:   Sun Apr 18 22:37:57 2021 +0800

    Merge branch 'abl_neo_test' of ssh://ssh.dev.azure.com/v3/e-os/device/caf-abl.tianocore.edk2 into abl_neo_test
```
