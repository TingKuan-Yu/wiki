# Purpose
We can crate a new branch from other commit in website. Then get the new branch locally for modification.


# operation
- get fetch
```
tingkuanyu@TonyYuLinux1:/D/c1/11/main/kernel_qgki/kernel/msm-5.4/techpack/audio$ git fetch device-caf personal/tony/device_switch:personal/tony/device_switch
From ssh://ssh.dev.azure.com/v3/e-os/device/caf-platform.vendor.opensource.audio-kernel
 * [new branch]        personal/tony/device_switch -> personal/tony/device_switch
 * [new branch]        personal/tony/device_switch -> device-caf/personal/tony/device_switch
```
- git checkout
```
tingkuanyu@TonyYuLinux1:/D/c1/11/main/kernel_qgki/kernel/msm-5.4/techpack/audio$ git checkout personal/tony/device_switch 
Previous HEAD position was 55814a9d dsp: ensure set persist cal type for TX path
Switched to branch 'personal/tony/device_switch'

```