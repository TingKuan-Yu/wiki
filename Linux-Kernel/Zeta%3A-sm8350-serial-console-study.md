# Enable console by
- change for user build
```
+CONFIG_MSM_GENI_SE=y
+CONFIG_SERIAL_MSM_GENI=y
+CONFIG_SERIAL_MSM_GENI_EARLY_CONSOLE=y
+CONFIG_SERIAL_MSM_GENI_HALF_SAMPLING=y
+CONFIG_IPC_LOGGING=y
```
- CONFIG_MSM_GENI_SE
  - obj-$(CONFIG_MSM_GENI_SE) += msm-geni-se.o
- CONFIG_SERIAL_MSM_GENI
  - obj-$(CONFIG_SERIAL_MSM_GENI) += msm_geni_serial.o
- CONFIG_SERIAL_MSM_GENI_EARLY_CONSOLE
  - obj-$(CONFIG_SERIAL_MSM_GENI_EARLY_CONSOLE) += msm_geni_serial_console.o
- CONFIG_SERIAL_MSM_GENI_HALF_SAMPLING=y
  - For baud rate.
- CONFIG_IPC_LOGGING if not set
```
[    2.803105] qupv3_geni_se 9c0000.qcom,qupv3_0_geni_se: geni_se_probe Failed to allocate log context
```

- check .config
  ```
  CONFIG_SERIAL_MSM_GENI=y
  CONFIG_SERIAL_MSM_GENI_EARLY_CONSOLE=y
  CONFIG_SERIAL_MSM_GENI_HALF_SAMPLING=y
  CONFIG_IPC_LOGGING=y
  ```


- msm-5.4/drivers/tty/serial/Makefile
```
obj-$(CONFIG_SERIAL_CORE) += serial_core.o
```

- msm-5.4/drivers/tty/serial/Kconfig
```
config SERIAL_CORE
	tristate

config SERIAL_MSM
	tristate "MSM on-chip serial port support"
	depends on ARCH_QCOM
	select SERIAL_CORE

config SERIAL_MSM_CONSOLE
	bool "MSM serial console support"
	depends on SERIAL_MSM=y
	select SERIAL_CORE_CONSOLE
	select SERIAL_EARLYCON

config SERIAL_MSM_GENI
	tristate "MSM on-chip GENI HW based serial port support"
	depends on ARCH_QCOM
	depends on MSM_GENI_SE
	select SERIAL_CORE
	help
	    Serial driver for Qualcomm Technologies Inc's GENI based QUPv3
	    hardware.
	    The driver supports console and High speed UART functions.

config SERIAL_MSM_GENI_EARLY_CONSOLE
	bool "MSM on-chip GENI HW based early console support"
	help
	    Serial early console driver for Qualcomm Technologies Inc's GENI
	    based QUP hardware.

config SERIAL_MSM_GENI_CONSOLE
	tristate "MSM on-chip GENI HW based console support"
	depends on SERIAL_MSM_GENI
	select SERIAL_CORE_CONSOLE
	select SERIAL_EARLYCON
	select SERIAL_MSM_GENI_EARLY_CONSOLE
	help
	    Serial console driver for Qualcomm Technologies Inc's GENI based
	    QUP hardware.

config SERIAL_MSM_GENI_HALF_SAMPLING
	bool "Changes clock divider which impacts sampling rate for QUP HW ver greater than 2.5.0"
	depends on SERIAL_MSM_GENI
	help
	  Clock divider value should be doubled for QUP hardware version
	  greater than 2.5.0.
	  As earlycon can't have HW version awareness, decision is taken
	  based on the configuration.

```