# git apply --reject --ignore-space-change --ignore-whitespace
 - generate .rej file once fail
 - work with "git am --continue" ?

# git apply PATCH --reject
  - edit edit edit
  - git add fixed file and remove rej file
  - git am --resolved
  - Abort method
    -  git am --abort
    - or "rm -rf .git/rebase-apply"


# git apply --reject --whitespace=fix 


# force remove
```
tingkuanyu@TonyYuLinux1:/D/c1/11/main/abl/bootable/bootloader/edk2$ git rm -f QcomModulePkg/Library/FastbootLib/MsFastbootCmds.h.rej
rm 'QcomModulePkg/Library/FastbootLib/MsFastbootCmds.h.rej'

```