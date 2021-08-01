# kernel/msm-5.4/Documentation/admin-guide/kernel-parameters.txt
## printk.devkmsg
- detail
```
	printk.devkmsg={on,off,ratelimit}
			Control writing to /dev/kmsg.
			on - unlimited logging to /dev/kmsg from userspace
			off - logging to /dev/kmsg disabled
			ratelimit - ratelimit the logging
			Default: ratelimit
```
- fastboot oem set-customized-kernel-param printk.devkmsg=on


# How to add more debug information in printk
  - CONFIG_PRINTK_CALLER
    https://marc.info/?l=linux-kernel&m=154508071805409&w=2
  - We shall add it in debug build for easily analyzing issues.


# kernel/msm-5.4/include/linux/device.h
- dev_dbg
```
#if defined(CONFIG_DYNAMIC_DEBUG) || \
	(defined(CONFIG_DYNAMIC_DEBUG_CORE) && defined(DYNAMIC_DEBUG_MODULE))
#define dev_dbg(dev, fmt, ...)						\
	dynamic_dev_dbg(dev, dev_fmt(fmt), ##__VA_ARGS__)
#elif defined(DEBUG)
#define dev_dbg(dev, fmt, ...)						\
	dev_printk(KERN_DEBUG, dev, dev_fmt(fmt), ##__VA_ARGS__)
#else
#define dev_dbg(dev, fmt, ...)						\
({									\
	if (0)								\
		dev_printk(KERN_DEBUG, dev, dev_fmt(fmt), ##__VA_ARGS__); \
})
#endif 
```

# Documentation/dynamic-debug-howto.txt
- dynamic
```
debugfs path sys/kernel/debug

1. dev_dbg uses dynamic_dev_dbg for printing log

CONFIG_DEBUG_FS=y   
CONFIG_DYNAMIC_DEBUG=y

3.adb shell command example

echo -n 'file dwc3-msm.c line 3440 +p'  >  <debugfs>/dynamic_debug/control

4. mount debugfs

mkdir /data/debugfs
mount -t debugfs none /data/debugfs

```