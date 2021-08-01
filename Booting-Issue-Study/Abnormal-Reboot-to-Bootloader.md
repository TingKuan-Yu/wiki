# core/init/service.cpp
- void Service::Reap(const siginfo_t& siginfo)
```
    // If we crash > 4 times in 4 minutes or before boot_completed,
    // reboot into bootloader or set crashing property
    boot_clock::time_point now = boot_clock::now();
    if (((flags_ & SVC_CRITICAL) || is_process_updatable) && !(flags_ & SVC_RESTART)) {
        bool boot_completed = android::base::GetBoolProperty("sys.boot_completed", false);
        if (now < time_crashed_ + 4min || !boot_completed) {
            if (++crash_count_ > 4) {
                if (flags_ & SVC_CRITICAL) {
                    // Aborts into bootloader
                    LOG(FATAL) << "critical process '" << name_ << "' exited 4 times "
                               << (boot_completed ? "in 4 minutes" : "before boot completed");
                } else {
                    LOG(ERROR) << "updatable process '" << name_ << "' exited 4 times "
                               << (boot_completed ? "in 4 minutes" : "before boot completed");
                    // Notifies update_verifier and apexd
                    SetProperty("sys.init.updatable_crashing_process_name", name_);
                    SetProperty("sys.init.updatable_crashing", "1");
                }
            }
        } else {
            time_crashed_ = now;
            crash_count_ = 1;
        }
    }

```

# Critical Service in .rc file
- https://android.googlesource.com/platform/system/core/+/master/init/README.md
  - critical [window=<fatal crash window mins>] [target=<fatal reboot target>]
    - This is a device-critical service. If it exits more than four times in fatal crash window mins minutes or before boot completes, the device will reboot into fatal reboot target. The default value of fatal crash window mins is 4, and default value of **fatal reboot target is ‘bootloader’**. For tests, the fatal reboot can be skipped by setting property init.svc_debug.no_fatal.<service-name> to true for specified critical service.