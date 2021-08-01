
# How to enable more kernel debug log (ex. for debugging init)
- https://dev.azure.com/DSQO-Taipei/Knowledge%20Share/_wiki/wikis/Knowledge-Share.wiki/82/How-to-enable-more-kernel-debug-log-(ex.-for-debugging-init)
  - fastboot oem set-customized-kernel-param printk.devkmsg=on
  - fastboot oem clear-customized-kernel-param

# Documentation/admin-guide/kernel-parameters.txt:
```
printk.devkmsg={on,off,ratelimit}
		Control writing to /dev/kmsg.
		on - unlimited logging to /dev/kmsg from userspace
		off - logging to /dev/kmsg disabled
		ratelimit - ratelimit the logging
		Default: ratelimit
```

# ./system/core/logd/logd.rc
```
service logd /system/bin/logd
    socket logd stream 0666 logd logd
    socket logdr seqpacket 0666 logd logd
    socket logdw dgram+passcred 0222 logd logd
    file /proc/kmsg r
    file /dev/kmsg w
    user logd
    group logd system package_info readproc
    capabilities SYSLOG AUDIT_CONTROL
    priority 10
    writepid /dev/cpuset/system-background/tasks
```