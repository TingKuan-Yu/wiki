
[[_TOC_]]


# XBL Uart Log: "usb: UFS Serial - 18b73f21"
- Get serial number from usb device or from soc. This number could be from USB device or from SOC.

```
QcomPkg/Include/Library/qusb_dci_common.h:
#define QUSB_DLOAD_INFO_ADDR_IN_IMEM            (SHARED_IMEM_USB_BASE)

QcomPkg/SocPkg/Lahaina/Library/QusbLdrLib/qusb_ldr_utils.c

static void qusb_fedl_update_usb_serial_string_and_cookie(void)
  :
  qusb_dload_info_type *dload_info_ptr = 
    (qusb_dload_info_type*)QUSB_DLOAD_INFO_ADDR_IN_IMEM;
  :

    else if(QUSB_FS_HOTPLUG_SUCCESS != coldplug_get_device_info(chdl, &dev_info))
    {
      qusb_uart_log("emmc/sdc_info_fail", 0);
    }
    else
    {
      serial_num = dev_info.product_serial_number;
    }

  :
  if (is_ufs_available)
  {
    qusb_uart_w_str_log("usb: UFS Serial", dload_info_ptr->serial_number);
  }
  else
  {
    qusb_uart_w_str_log("usb: Serial", dload_info_ptr->serial_number);
  }
```