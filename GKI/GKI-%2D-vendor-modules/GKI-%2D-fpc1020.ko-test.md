# adb push QGKI fpc1020.ko to /data/loca/tmp of GKI device
``` 
tingkuanyu@TonyYuLinux1:/E/GKI/kernel/out/target/product/oemc1/dlkm$ adb push ./lib/modules/fpc1020.ko /data/local/tmp
```

# insmod fpc1020.ko
```
1|c1:/data/local/tmp # insmod fpc1020.ko                                                                                                                                                                          
insmod: failed to load fpc1020.ko: Exec format error
1|c1:/data/local/tmp # dmesg | grep fpc
[ 2069.161832] fpc1020: disagrees about version of symbol module_layout
c1:/data/local/tmp # find /vendor/lib/modules | grep fpc1020.ko                                                                                                                                                   
/vendor/lib/modules/5.4-gki/fpc1020.ko
c1:/data/local/tmp # insmod /vendor/lib/modules/5.4-gki/fpc1020.ko
insmod: failed to load /vendor/lib/modules/5.4-gki/fpc1020.ko: File exists
1|c1:/data/local/tmp # lsmod | grep fpc1020
fpc1020                28672  0 
c1:/data/local/tmp # uname -a     
Linux localhost 5.4.86-c1-g-0_0_0 #1 SMP PREEMPT Mon Jun 21 06:09:58 UTC 2021 aarch64
c1:/data/local/tmp # lsmod | grep fpc1020
fpc1020                28672  0 

127|c1:/data/local/tmp # rmmod fpc1020                                                                                                                                                                            
c1:/data/local/tmp # modinfo /vendor/lib/modules/5.4-gki/fpc1020.ko
filename:       /vendor/lib/modules/5.4-gki/fpc1020.ko
author:         Aleksej Makarov
author:         Henrik Tillman <henrik.tillman@fingerprints.com>
description:    FPC1020 Fingerprint sensor device driver.
vermagic:       5.4.86-c1-g-0_0_0 SMP preempt mod_unload modversions aarch64
intree:         Y
depends:        
alias:          of:N*T*Cfpc,fpc1020
alias:          of:N*T*Cfpc,fpc1020C*
c1:/data/local/tmp # insmod /vendor/lib/modules/5.4-gki/fpc1020.ko
c1:/data/local/tmp # lsmod | grep fpc1020                                                                                                                                                                         
fpc1020                28672  0 
c1:/data/local/tmp # rmmod fpc1020                                                                                                                                                                                
c1:/data/local/tmp # modinfo fpc1020.ko                                                                                                                                                                           
filename:       fpc1020.ko
author:         Aleksej Makarov
author:         Henrik Tillman <henrik.tillman@fingerprints.com>
description:    FPC1020 Fingerprint sensor device driver.
vermagic:       5.4.86-c1-p-0_0_0 SMP preempt mod_unload modversions aarch64
intree:         Y
depends:        
alias:          of:N*T*Cfpc,fpc1020
alias:          of:N*T*Cfpc,fpc1020C*
c1:/data/local/tmp # insmod fpc1020.ko                                                                                                                                                                            
insmod: failed to load fpc1020.ko: Exec format error
1|c1:/data/local/tmp # dmesg | grep fpc1020
[ 2069.161832] fpc1020: disagrees about version of symbol module_layout
[ 2599.115147] fpc1020_exit
[ 2599.115206] fpc1020 soc:fpc1020: fpc1020_remove
[ 2625.938388] fpc1020 soc:fpc1020: found pin control fpc1020_reset_reset
[ 2625.938393] fpc1020 soc:fpc1020: found pin control fpc1020_reset_active
[ 2625.938396] fpc1020 soc:fpc1020: found pin control fpc1020_irq_active
[ 2625.953122] fpc1020 soc:fpc1020: IRQ before reset 0
[ 2625.963798] fpc1020 soc:fpc1020: IRQ after reset 1
[ 2625.963805] fpc1020 soc:fpc1020: fpc1020_probe: ok
[ 2625.964876] fpc1020_init OK
[ 2635.059634] fpc1020_exit
[ 2635.059696] fpc1020 soc:fpc1020: fpc1020_remove
[ 2694.468981] fpc1020: disagrees about version of symbol module_layout

```