# reference
  - https://dev.azure.com/DSQO-Taipei/Knowledge%20Share/_wiki/wikis/Knowledge-Share.wiki/135/Modify-manifest-for-signed-image

# clone and set branch
- personal/tony/uefi_test
```
tingkuanyu@TonyYuLinux1:/D/c1/11/main/multi-pr/GKI$ git clone git@ssh.dev.azure.com:v3/E-OS/device/manifest uefi_manifest
Cloning into 'uefi_manifest'...
remote: Azure Repos
remote: Found 21777 objects to send. (349 ms)
Receiving objects: 100% (21777/21777), 5.81 MiB | 1.03 MiB/s, done.
Resolving deltas: 100% (13976/13976), done.
tingkuanyu@TonyYuLinux1:/D/c1/11/main/multi-pr/GKI$ cd uefi_manifest/
tingkuanyu@TonyYuLinux1:/D/c1/11/main/multi-pr/GKI/uefi_manifest$ git branch personal/tony/uefi_test
tingkuanyu@TonyYuLinux1:/D/c1/11/main/multi-pr/GKI/uefi_manifest$ git checkout personal/tony/uefi_test
Switched to branch 'personal/tony/uefi_test'
```

# Seem unnecessary to creat a own sign branch
- build abl/xbl for unfused device test
- push to ADO and create a pr
- use pr to run multi-pr pipeline for nonhlos only, then we can get sign abl.
