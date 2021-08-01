# Library/FastbootLib/FastbootCmds.c
```
#ifndef SHIP_MODE
      {"oem set-adb-kernel-param", CmdOemSetAdbKernelParam}, // MS_CHANGE
      {"oem clear-adb-kernel-param", CmdOemClearAdbKernelParam}, // MS_CHANGE
      {"oem set-maxcpu-kernel-param", CmdOemSetMaxCpuKernelParam}, // MS_CHANGE
      {"oem clear-maxcpu-kernel-param", CmdOemClearMaxCpuKernelParam}, // MS_CHANGE
      {"oem set-setupwiz-kernel-param", CmdOemSetSetupwizKernelParam}, // MS_CHANGE
      {"oem clear-setupwiz-kernel-param", CmdOemClearSetupwizKernelParam}, // MS_CHANGE
      {"oem clear-force-normal-boot", CmdClearForceNormalBoot}, // MS_CHANGE
      {"oem set-force-normal-boot", CmdSetForceNormalBoot}, // MS_CHANGE
      {"oem set-selinux-permissive-kernel-param", CmdOemSetSeLinuxPermissiveKernelParam}, // MS_CHANGE
      {"oem clear-selinux-permissive-kernel-param", CmdOemClearSeLinuxPermissiveKernelParam}, // MS_CHANGE
      {"oem get-random-number-generator", CmdOemRandomNumberGenerator}, // MS_CHANGE
      {"oem set-customized-kernel-param", CmdOemSetCustomizedKernelParam}, // MS_CHANGE
      {"oem extend-customized-kernel-param", CmdOemExtendCustomizedKernelParam}, // MS_CHANGE
      {"oem clear-customized-kernel-param", CmdOemClearCustomizedKernelParam}, // MS_CHANGE
      {"oem set-soc-debug-mux", CmdOemSetSocDebugMux }, // MS_CHANGE
      {"oem set-touch-debug-mux", CmdOemSetTouchDebugMux }, // MS_CHANGE
      {"oem clear-debug-mux", CmdOemClearDebugMux }, // MS_CHANGE
#endif // SHIP_MODE
```
# "oem set-customized-kernel-param"
 - add strings in command line as kernel parameters
 - example
   - fastboot oem set-customized-kernel-param printk.devkmsg=on
     - Add a "printk.devkmsg" kernel command line parameter which controls how
       **userspace** writes into /dev/kmsg.  It has three options:
       * ratelimit - ratelimit logging from userspace.
       * on  - unlimited logging from userspace
       * off - logging from userspace gets ignored
       
        The default setting is to ratelimit the messages written to it.


# "oem clear-customized-kernel-param"