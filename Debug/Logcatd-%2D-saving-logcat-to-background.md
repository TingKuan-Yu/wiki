[[_TOC_]]

# Test
---
- image version
```
duo2:/data/misc/logd # getprop | grep fingerprint
[ro.bootimage.build.fingerprint]: [surface/duo2/duo2:11/2021.711.8/202107110008:user/release-keys]
[ro.build.fingerprint]: [surface/duo2/duo2:11/2021.711.8/202107110008:user/release-keys]
[ro.odm.build.fingerprint]: [surface/duo2/duo2:11/2021.711.8/202107110008:user/release-keys]
[ro.product.build.fingerprint]: [surface/duo2/duo2:11/2021.711.8/202107110008:user/release-keys]
[ro.system.build.fingerprint]: [surface/duo2/duo2:11/2021.711.8/202107110008:user/release-keys]
[ro.system_ext.build.fingerprint]: [surface/duo2/duo2:11/2021.711.8/202107110008:user/release-keys]
[ro.vendor.build.fingerprint]: [surface/duo2/duo2:11/2021.711.8/202107110008:user/release-keys]
```
- check log in /data/misc/logd after booting
  - no log
```
duo2:/data/misc/logd # ls
event-log-tags
duo2:/data/misc/logd # cat event-log-tags                                                                                                                                                                  
duo2:/data/misc/logd # ps -Alf | grep logcat
root           4423   4378 3 22:13:21 pts/0 00:00:00 grep logcat
```
**- start logcatd**
```
duo2:/data/misc/logd # start logcatd
duo2:/data/misc/logd # ls   
event-log-tags  logcat  logcat.001  logcat.id
duo2:/data/misc/logd # ps -Alf | grep logcat
logd           4466      1 1 22:15:52 ?     00:00:00 logcat -b all -v threadtime -v usec -v printable -D -f /data/misc/logd/logcat -r 2048 -n 256 --id=2021.711.8
root           4500   4378 3 22:17:19 pts/0 00:00:00 grep logcat
```

# system/core/logcat/logcatd.rc
---
- logcatd service
  - default **disabled**
```
on property:logd.logpersistd.enable=true && property:logd.logpersistd=logcatd
    # log group should be able to read persisted logs
    mkdir /data/misc/logd 0750 logd log
    start logcatd

service logcatd /system/bin/logcatd -L -b ${logd.logpersistd.buffer:-all} -v threadtime -v usec -v printable -D -f /data/misc/logd/logcat -r ${logd.logpersistd.rotate_kbytes:-2048} -n ${logd.logpersistd.size:-256} --id=${ro.build.id}
    class late_start
    disabled
    # logd for write to /data/misc/logd, log group for read from log daemon
    user logd
    group log
    writepid /dev/cpuset/system-background/tasks
    oom_score_adjust -600
```
## **setprop logd.logpersistd ** 
  - logcatd, stop or clear
```
duo2:/data/misc/logd # ls
event-log-tags
duo2:/data/misc/logd # getprop | grep logd.logpersistd
[logd.logpersistd.enable]: [true]
[persist.logd.logpersistd]: []

duo2:/data/misc/logd # setprop logd.logpersistd logcatd                                                                                                                                                    
duo2:/data/misc/logd # ps -Alf | grep logcat                                                                                                                                                               
logd           4546      1 8 22:19:41 ?     00:00:00 logcat -b all -v threadtime -v usec -v printable -D -f /data/misc/logd/logcat -r 2048 -n 256 --id=2021.711.8
root           4551   4426 3 22:19:43 pts/0 00:00:00 grep logcat
duo2:/data/misc/logd # ls                                                                                                                                                                                  
event-log-tags  logcat  logcat.001  logcat.id
duo2:/data/misc/logd # setprop logd.logpersistd stop                                                                                                                                                       
duo2:/data/misc/logd # ps -Alf | grep logcat                                                                                                                                                               
root           4560   4426 1 22:20:06 pts/0 00:00:00 grep logcat
duo2:/data/misc/logd # ls  
event-log-tags  logcat  logcat.001  logcat.id

duo2:/data/misc/logd # setprop logd.logpersistd logcatd
duo2:/data/misc/logd # ls
event-log-tags  logcat  logcat.001  logcat.id
duo2:/data/misc/logd # setprop logd.logpersistd clear                                                                                                                                                      
duo2:/data/misc/logd # ls
event-log-tags  logcat.id
```
- Refer to https://developer.android.com/studio/command-line/logcat?hl=zh-tw & https://developer.android.com/studio/command-line/logcat?hl=zh-tw#outputFormat for parameter
  - -b <buffer>	Load an alternate log buffer for viewing, such as events or radio. The main, system, and crash buffer set is used by default. See Viewing Alternative Log Buffers.
  - -v <format>	Set the output format for log messages. The default is threadtime format. For a list of supported formats, go to the section about the Control log output format.
    - thread: A legacy format that shows priority, PID, and TID of the thread issuing the message.
    - usec: Display the time with precision down to microseconds.
    - printable: Ensure that any binary logging content is escaped.
  - -D, --dividers	Print dividers between each log buffer.
  - -f <filename>	Write log message output to <filename>. The default is stdout.
  - -r <kbytes>	Rotate the log file every <kbytes> of output. The default value is 16. Requires the -f option.
  - -n <count>	Set the maximum number of rotated logs to <count>. The default value is 4. Requires the -r option.
  - --id
    ```
    duo2:/data/misc/logd # cat logcat.id                                                                                                                                                                       
    2021.711.8
    ```

# Sepolicy for logpersistd
---
## Sepolicy of /data/misc/logd
- test
```
duo2:/data/misc # ls -alZ | grep logd                                                                                                                                                                      
drwxr-x---  2 logd         log          u:object_r:misc_logd_file:s0               3452 2021-07-11 22:15 logd
```
- system/sepolicy/public/init.te
```
# Init will create /data/misc/logd when the property persist.logd.logpersistd is "logcatd".
# Init will also walk through the directory as part of a recursive restorecon.
allow init misc_logd_file:dir { add_name open create read getattr setattr search write };
allow init misc_logd_file:file { open create getattr setattr write };
```

## getprop -Z | grep logpersistd
- u:object_r:logpersistd_logging_prop:s0
```
duo2:/data/misc/logd # getprop -Z | grep logpersistd                                                                                                                                                       
[logd.logpersistd.enable]: [u:object_r:logpersistd_logging_prop:s0]
[persist.logd.logpersistd]: [u:object_r:logpersistd_logging_prop:s0]
```
# system/sepolicy/public/property.te
```
system_public_prop(logpersistd_logging_prop)

neverallow { domain -coredomain } {
  system_property_type
  -system_public_property_type
}:property_service set;
```

## system/sepolicy/public/shell.te
```
# logpersist script
userdebug_or_eng(`set_prop(shell, logpersistd_logging_prop)')
```

# system/sepolicy/private/system_app.te
- only allow userdebug or eng to set logpersistd_logging_prop
```
userdebug_or_eng(`set_prop(system_app, logpersistd_logging_prop)')
```