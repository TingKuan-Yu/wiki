[[_TOC_]]

# UTF repo
---
- https://dev.azure.com/E-OS/tools/_git/utf-subsystems
- git clone - git@ssh.dev.azure.com:v3/E-OS/tools/utf-subsystems
```
tingkuanyu@TonyYuLinux1:/E/utf$ git clone git@ssh.dev.azure.com:v3/E-OS/tools/utf-subsystems
Cloning into 'utf-subsystems'...
:
```

# Setup environment before running test
---
- source testsetup.sh 
```
bsp@bsp-build-server:/media/bsp/disk3/tonyyu/uft/utf-subsystems$ source testsetup.sh 
/media/bsp/disk3/tonyyu/uft/utf-subsystems /media/bsp/disk3/tonyyu/uft/utf-subsystems
Building tests...
az artifacts universal download \
                --organization "https://dev.azure.com/E-OS/" \
                --feed "utf-duodependencies-main" \
                --name "duodependencies" \
                --version "`cat duodependencies-ver.txt`" \
                --path out/artifacts
 - Downloading ..
:
```

# Run utf test
---
## tricky method to avoid running CTS test
- by rename utf-cts.yaml to ut-f-cts.yaml
```
tingkuanyu@TonyYuLinux1:/E/utf/utf-subsystems$ mv yamltests/cts/utf-cts.yaml yamltests/cts/ut-f-cts.yaml
```

## Run test
- use "make tests" to run utf test locally
```
tingkuanyu@TonyYuLinux1:/E/utf/utf-subsystems$ make tests
```
