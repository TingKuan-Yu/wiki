# Task
- https://dev.azure.com/E-OS/Zeta/_sprints/taskboard/UEFI/Zeta/Software%20Iteration/Backlog/2021/Sprint%2015%20(7-11-2021%20-%207-23-2021)?workitem=178009

# QCT Document 
## Minidump Introduction 80-PN330-3 Rev. B
  - How BOOT will differentiate between Full dump & Minidump
    Using the register TCSR_TCSR_BOOT_MISC_DETECT(**0x01FD3000**). Bit positions :
     #define SBL_DLOAD_MODE_BIT_MASK 0x00000010
     #define SBL_MINIDUMP_MODE_BIT_MASK 0x00000020
    - related to **/sys/kernel/dload/dload_mode**
  - How BOOT will decide dump location (eMMC or SD-Card or QPST)
     Boot will check the cookies in this order : Raw partition -> SD Card -> QPST
     Raw partition Cookie : **0x146BF01C** (boot_shared_imem_cookie_ptr->uefi_ram_dump_magic)
     SD Card Cookie : RTCookie.txt and RDCookie.txt
    - related to **/sys/kernel/dload/emmc_dload**
## Other related docs
  - Minidump Software User Guide 80-P8754-71 Rev. F April 9, 2021 

# device tree
## vendor/qcom/proprietary/devicetree/qcom/lahaina.dtsi
- qcom,msm-imem@**146bf000**
  - dload_type --> **146bf01c**
```
qcom,msm-imem@146bf000 {
		compatible = "qcom,msm-imem";
		reg = <0x146bf000 0x1000>;
		ranges = <0x0 0x146bf000 0x1000>;
:
		dload_type@1c {
			compatible = "qcom,msm-imem-dload-type";
			reg = <0x1c 0x4>;
		};
:
}
```

# Kernel
## kernel/msm-5.4/include/linux/qcom_scm.h
-  enum qcom_download_mode
```
enum qcom_download_mode {
	QCOM_DOWNLOAD_NODUMP	= 0x00,
	QCOM_DOWNLOAD_EDL	= 0x01,
	QCOM_DOWNLOAD_FULLDUMP	= 0x10,
	QCOM_DOWNLOAD_MINIDUMP	= 0x20,
};
```

## kernel/msm-5.4/drivers/power/reset/msm-poweroff.c
- dload_type: SCM_DLOAD_FULLDUMP, SCM_DLOAD_MINIDUMP, SCM_DLOAD_BOTHDUMPS
```
#define SCM_DLOAD_FULLDUMP		QCOM_DOWNLOAD_FULLDUMP
#define SCM_DLOAD_MINIDUMP		QCOM_DOWNLOAD_MINIDUMP
#define SCM_DLOAD_BOTHDUMPS	(SCM_DLOAD_FULLDUMP | SCM_DLOAD_MINIDUMP)
```

- download_mode: 1 or 0   
  - default enabled
```
static int download_mode = 1;
```

- static int msm_restart_probe(struct platform_device *pdev)
 1. No 'reg-names = "pshold-base", "tcsr-boot-misc-detect"' in dtsi for sm8350, so **tcsr_boot_misc_detect is not defined**.
  NOte: sm8150 has resource definition in dtsi
        vendor/qcom/proprietary/devicetree/qcom/sm8150.dtsi
      	reg-names = "pshold-base", "tcsr-boot-misc-detect";
```
	mem = platform_get_resource_byname(pdev, IORESOURCE_MEM, "pshold-base");
	msm_ps_hold = devm_ioremap_resource(dev, mem);
	if (IS_ERR(msm_ps_hold))
		return PTR_ERR(msm_ps_hold);

	mem = platform_get_resource_byname(pdev, IORESOURCE_MEM,
					   "tcsr-boot-misc-detect");
	if (mem)
		tcsr_boot_misc_detect = mem->start;
```
 2. default set to mini dump --> dload_type = SCM_DLOAD_MINIDUMP;
```
	// MSCHANGE START
	// Setting DLOAD mode to minidump and enabling EMMC_DLOAD.
	// This will help the device go into minidump mode if there
	// is a crash between this driver and the init script for changing
	// the cookie based on build flavour
	dload_type = SCM_DLOAD_MINIDUMP;
	set_dload_mode(download_mode);
	if (dload_type_addr)
		__raw_writel (EMMC_DLOAD_TYPE, dload_type_addr);
	// MSCHANGE ENDS
```


- static void *map_prop_mem(const char *propname)
  - find device tree node and use of_iomap to get address
  - DL_MODE_PROP --> not defined in device tree for sm8350 platform
  - EDL_MODE_PROP --> not defined in device tree for sm8350 platform
  - **IMEM_DL_TYPE_PROP --> define in vendor/qcom/proprietary/devicetree/qcom/lahaina.dtsi**
```
#define DL_MODE_PROP "qcom,msm-imem-download_mode"
#define EDL_MODE_PROP "qcom,msm-imem-emergency_download_mode"
#define IMEM_DL_TYPE_PROP "qcom,msm-imem-dload-type"

static void *map_prop_mem(const char *propname)
{
	struct device_node *np = of_find_compatible_node(NULL, NULL, propname);
	void *addr;

	if (!np) {
		pr_err("Unable to find DT property: %s\n", propname);
		return NULL;
	}

	addr = of_iomap(np, 0);
	if (!addr)
		pr_err("Unable to map memory for DT property: %s\n", propname);

	return addr;
}
```

- static void setup_dload_mode_support(void)
  - call by msm_restart_probe()
  - only dload_type_addr is defined.
```
dload_mode_addr = map_prop_mem(DL_MODE_PROP);
emergency_dload_mode_addr = map_prop_mem(EDL_MODE_PROP);
dload_type_addr = map_prop_mem(IMEM_DL_TYPE_PROP);
```

- static void set_dload_mode(int on)
  - dload_mode_addr 
    - according to qualcomm doc, we are using TCSR but not this address.
    - The dlad_mode_addr is 0, so these two values will not be wrote to it.
  - qcom_scm_set_download_mode() 
    - set dload_type
    - tcsr_boot_misc_detect is 0
```
	if (dload_mode_addr) {
		__raw_writel(on ? 0xE47B337D : 0, dload_mode_addr);
		__raw_writel(on ? 0xCE14091A : 0,
		       dload_mode_addr + sizeof(unsigned int));
		/* Make sure the download cookie is updated */
		mb();
	}

	qcom_scm_set_download_mode(on ? dload_type : 0,
				   tcsr_boot_misc_detect ? : 0);

	dload_mode_enabled = on;
```

- store_dload_mode()
  - export /sys/kernel/dload/dload_mode for setting
```
static size_t store_dload_mode(struct kobject *kobj, struct attribute *attr,
			       const char *buf, size_t count);
RESET_ATTR(dload_mode, 0644, show_dload_mode, store_dload_mode);

static size_t store_dload_mode(struct kobject *kobj, struct attribute *attr,
				const char *buf, size_t count)
{
	if (sysfs_streq(buf, "full")) {
		dload_type = SCM_DLOAD_FULLDUMP;
	} else if (sysfs_streq(buf, "mini")) {
		if (!msm_minidump_enabled()) {
			pr_err("Minidump is not enabled\n");
			return -ENODEV;
		}
		dload_type = SCM_DLOAD_MINIDUMP;
	} else if (sysfs_streq(buf, "both")) {
		if (!msm_minidump_enabled()) {
			pr_err("Minidump not enabled, setting fulldump only\n");
			dload_type = SCM_DLOAD_FULLDUMP;
			return count;
		}
		dload_type = SCM_DLOAD_BOTHDUMPS;
	} else {
		pr_err("Invalid Dump setup request..\n");
		pr_err("Supported dumps:'full', 'mini', or 'both'\n");
		return -EINVAL;
	}

	mutex_lock(&tcsr_lock);
	/*Overwrite TCSR reg*/
	set_dload_mode(dload_type);
	mutex_unlock(&tcsr_lock);
	return count;
}

```

## kernel/msm-5.4/drivers/firmware/qcom_scm.c
- qcom_scm_set_download_mode()
  - tcsr_boot_misc --> 0
  - qcom_scm_probe() --> __scm = scm;
  - __scm->dload_mode_addr --> from device tree "qcom,dload-mode"
    - qcom_scm_probe() --> ret = qcom_scm_find_dload_address(&pdev->dev, &scm->dload_mode_addr);
  - __qcom_scm_io_writel() --> write mode to __scm->dload_mode_addr
```
void qcom_scm_set_download_mode(enum qcom_download_mode mode,
				phys_addr_t tcsr_boot_misc)
{
	int ret = -EINVAL;
	struct device *dev = __scm ? __scm->dev : NULL;

	if (tcsr_boot_misc || (__scm && __scm->dload_mode_addr)) {
		ret = __qcom_scm_io_writel(dev,
				tcsr_boot_misc ? : __scm->dload_mode_addr,
				mode);
	} else
		ret = __qcom_scm_set_dload_mode(dev, mode);

	if (ret)
		dev_err(dev, "failed to set download mode: %d\n", ret);
}
EXPORT_SYMBOL(qcom_scm_set_download_mode);
```
- qcom_scm_find_dload_address() --> **0x01FD3000**
  - vendor/qcom/proprietary/devicetree/qcom/lahaina.dtsi
    -	tcsr: syscon@1fc0000 {
		compatible = "syscon";
		reg = <0x1fc0000 0x30000>;
	};
    - 	scm {
		compatible = "qcom,scm";
		qcom,dload-mode = <&tcsr 0x13000>;
	};
```
static int qcom_scm_find_dload_address(struct device *dev, u64 *addr)
{
	struct device_node *tcsr;
	struct device_node *np = dev->of_node;
	struct resource res;
	u32 offset;
	int ret;

	tcsr = of_parse_phandle(np, "qcom,dload-mode", 0);
	if (!tcsr)
		return 0;

	ret = of_address_to_resource(tcsr, 0, &res);
	of_node_put(tcsr);
	if (ret)
		return ret;

	ret = of_property_read_u32_index(np, "qcom,dload-mode", 1, &offset);
	if (ret < 0)
		return ret;

	*addr = res.start + offset;

	return 0;
}
```

# Vendor
## vendor/surface/crashdump/mdCollectord.rc
- Set to different download mode according to ro.build.type
```
on property:ro.build.type=eng
  write /sys/kernel/dload/dload_mode full
  write /sys/kernel/dload/emmc_dload 0

on property:ro.build.type=userdebug
  write /sys/kernel/dload/dload_mode full
  write /sys/kernel/dload/emmc_dload 0

on property:ro.build.type=user
  write /sys/kernel/dload/dload_mode mini
  write /sys/kernel/dload/emmc_dload 1
```

# XBL - check ramdump
## BOOT.MXF.1.0/boot_images/boot/QcomPkg/SocPkg/Lahaina/Common/uefiplat.cfg
```
DloadCookieAddr = 0x01FD3000
# for full dump 0x10, for minidump 0x20
DloadCookieValue = 0x10
```

## BOOT.MXF.1.0/boot_images/boot/QcomPkg/XBLCore/UefiPlatCfg.c
- Load uefiplat.cfg to CfgBuffer for futher using.
```
#define UEFIPLATCFG_FILE "uefiplat.cfg"
LoadAndParsePlatformCfg ( VOID )
{
:
  Status = LoadFileFromFV0 (UEFIPLATCFG_FILE, &CfgBuffer, &FileSize);
}
```


# XBL - save ramdump to rawdump
## Dump location  - 0x146BF000
- Base address of IMEM to save cookie

## define memory section
- boot_images/boot/QcomPkg/SocPkg/Lahaina/Common/**Core.fdf**
```
  FILE FREEFORM = DDE58710-41CD-4306-DBFB-3FA90BB1D2DD {
    SECTION UI = "uefiplat.cfg"
    SECTION RAW = QcomPkg/SocPkg/Lahaina/Common/uefiplat.cfg
  }

```
- boot_images/boot/QcomPkg/SocPkg/Lahaina/Common/**uefiplat.cfg**
- IMEI Cookei Base
```
0x146BF000, 0x00001000, "IMEM Cookie Base",   AddDev, MMAP_IO, INITIALIZED, Conv,   NS_DEVICE

# Shared IMEM (Cookies, Offsets)
SharedIMEMBaseAddr    = 0x146BF000
```

## BOOT.MXF.1.0/boot_images/boot/QcomPkg/SocPkg/Lahaina/Common/Core.dsc.inc
```
  gQcomTokenSpaceGuid.PcdIMemCookiesBase|0x146BF000
  gQcomTokenSpaceGuid.PcdIMemCookiesSize|0x00001000
```

## BOOT.MXF.1.0/boot_images/boot/QcomPkg/Drivers/CrashDumpDxe/CrashDumpDxe.inf
```
[Pcd]
  gQcomTokenSpaceGuid.PcdIMemCookiesBase
```

## BOOT.MXF.1.0/boot_images/boot/QcomPkg/Drivers/CrashDumpDxe/CrashDumpDxe.c
- InitializeResetDataBuffers ( EFI_OFFLINE_CRASHDUMP_CONFIG_TABLE *mOfflineCrashDumpConfigTable )
  - **boot_shared_imem_cookie_ptr**
```
/*Define a global pointer which points to the boot shared imem cookie structure */
struct boot_shared_imem_cookie_type *boot_shared_imem_cookie_ptr = NULL;

InitializeResetDataBuffers ( EFI_OFFLINE_CRASHDUMP_CONFIG_TABLE *mOfflineCrashDumpConfigTable )
{
:
  boot_shared_imem_cookie_ptr = (struct boot_shared_imem_cookie_type *)((UINT64)PcdGet32(PcdIMemCookiesBase));

:
}
```

## BOOT.MXF.1.0/boot_images/boot/QcomPkg/Include/Library/boot_shared_imem_cookie.h
```
/* 
 * Following structure defines all the cookies that have been placed 
 * in boot's shared imem space.
 * The size of this struct must NOT exceed SHARED_IMEM_BOOT_SIZE
 */
struct boot_shared_imem_cookie_type
{
:
  /* Magic number for UEFI ram dump, if this cookie is set along with dload magic numbers,
     we don't enter dload mode but continue to boot. This cookie should only be set by UEFI*/
  uint32 uefi_ram_dump_magic;
:
};

```

## BOOT.MXF.1.0/boot_images/boot/QcomPkg/XBLRamDump/boot_raw_partition_ramdump.c
- void boot_ram_dump_to_raw_parition(boot_handle config_context_handle)
  - dload_mem_debug_supported()
    - boot_dload_debug_target.c -> seccfg_if->qsee_is_memory_dump_allowed(...)
```
*  This routine Checks for the raw partition ram dump cookie 
*  and initiate the ram dumps to raw partition. It will reset the device
*  in case of succesful ram dump or in error of insufficent storage.
:
*/
void boot_ram_dump_to_raw_parition(boot_handle config_context_handle)
{
:
  /* Only perform ram dump if uefi dump cookie is set AND 
     memory debug is allowed */
  if((boot_shared_imem_cookie_ptr != NULL) &&
     (boot_shared_imem_cookie_ptr->uefi_ram_dump_magic == BOOT_RAW_RAM_DUMP_MAGIC_NUM) &&
     dload_mem_debug_supported())
  {
    DL_LOG("Raw Partition Dump");

:
}
```


