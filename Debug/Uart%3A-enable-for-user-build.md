# Set below config to y in kernel config
- CONFIG_MSM_GENI_SE=y
- CONFIG_SERIAL_MSM_GENI=y
- SERIAL_MSM_GENI_HALF_SAMPLING=y
- SERIAL_MSM_GENI_EARLY_CONSOLE=y
- CONFIG_SERIAL_MSM_GENI_CONSOLE=y

#  remove ro.debuggable in system init.rc
```
on init && property:ro.debuggable=1  --> on init
    start console
```