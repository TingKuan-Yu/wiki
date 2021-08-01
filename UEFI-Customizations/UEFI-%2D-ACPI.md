UEFI 好像可以拿到?
boot_images/boot/QcomPkg/Include/Protocol/EFIAcpiPlatform.h

struct _EFI_QCOM_ACPIPLATFORM_PROTOCOL {
   UINT64                                            Revision;
   EFI_ACPIPLATFORM_PROTOCOL_GET_ACPI_TABLE          GetAcpiTable;
   EFI_ACPIPLATFORM_PROTOCOL_GET_ACPI_TABLE_SIZE     GetAcpiTableSize;
   EFI_ACPI_PLATFORM_REGISTER                        AcpiTableRegister;
   EFI_ACPI_AML_VARIABLE_REGISTER                    AmlVariableRegister;
   EFI_ACPI_REGISTER_DEVICES_FOR_DSDT_STA_PATCH      AmlRegisterDevicesForDsdtStaPatch;
}

[11:09 AM] Amy Tang
    
c1:/ # acpi --help                                                                                                                                                                                         
usage: acpi [-abctV]


Show status of power sources and thermal devices.


-a    Show power adapters
-b    Show batteries
-c    Show cooling device state
-t    Show temperatures
-V    Show everything
 




​[11:09 AM] Amy Tang
    但好像都不是table???
​[11:09 AM] Amy Tang
    我-V 出來一堆東西XDD
​[11:10 AM] Amy Tang
    哪一個是要的阿XD
​[11:11 AM] Amy Tang
    看起來都不像 OTZ 一堆thermal cooling之類的
​[11:12 AM] William Wu
    我覺得在Arm ACPI table 應該是變成device tree了
​[11:13 AM] William Wu
    要看Donna要看什麼資訊
