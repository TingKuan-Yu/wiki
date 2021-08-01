# sync lahaina_GKI.config to hi2020 lahaina_GKI.config

## move CONFIG_HZ_1000=y to lahaina_QGKI.config
- This config is not defined in lahaina_GKI.config of hi2020, so move to lahaina_QGKI.config
- related PR
```
Author: Felipe Balbi <febalbi@microsoft.com>  2020-11-21 01:21:21
    Merged PR 16312: ARM64: config: lahaina: enable CONFIG_HZ_1000
    ARM64: config: lahaina: enable CONFIG_HZ_1000
    We want a low latency desktop behavior
```

## move CONFIG_FPR_FPC=y to lahaina_QGKI.config
- This config is not defined in lahaina_GKI.config of hi2020, so move to lahaina_QGKI.config
- related PR
```
Author: Elyas Razzaghi <v-elrazz@microsoft.com>  2020-08-20 17:32:07
    Merged PR 12416: fpc:fingerprint driver and dts integration   
    fpc:fingerprint driver and dts integration
```

## move CONFIG_ARCH_YUPIK=n to lahaina_QGKI.config
- This config is not defined in lahaina_GKI.config of hi2020, so move to lahaina_QGKI.config
- related PR
```
Author: William Wu <fangruwu@microsoft.com>  2021-02-21 18:15:50
Precedes: 

    dont build unused arch
```

## move CONFIG_DEBUG_STACK_USAGE=y and CONFIG_DEBUG_MEMORY_INIT=y to lahaina_QGKI.config
- These configs are not defined in lahaina_GKI.config of hi2020, so move to lahaina_QGKI.config
- related PR
```
Author: Vijay Lamba <vlamba@microsoft.com>  2021-03-15 20:12:19

    Merged PR 21576: removing some configs from user builds
    
    Removed following 2 configs from user builds :
    CONFIG_DEBUG_STACK_USAGE
    CONFIG_DEBUG_MEMORY_INIT
    To optimize kernel.

```