Comment
Created By: Padmaneela Nallani (7/22/2021 9:21 PM)
Dear customer,

Please help us to close the case if you don't have further queries.

Thanks,
Padmaneela
Created By: Astha Keshan (7/22/2021 6:01 PM)
Thanks!
Created By: Padmaneela Nallani (7/16/2021 3:59 AM)
Dear customer,

If I add this line to uefiplat.cfg: +SecurityFlag = 0x1C4

with this changes qseelogs will come in uart, for tz logs we need to crash the device and collect dump.

do you have any tool to parse dumps? using same you can parse tzlogs.
but tzlogs you need to share with qcom to analysis. let us know your requirement fot tz logs if any


Thanks,
Padmaneela
Created By: Astha Keshan (7/15/2021 11:24 AM)
Thanks Padmaneela!

If I add this line to uefiplat.cfg:
+SecurityFlag = 0x1C4

then will it just print TZ logs to UART/serial directly?

Or do I need to crash the device? And if I do need to crash it then how can I extract the log from the dump collected?

Thanks,
Astha
Created By: Padmaneela Nallani (7/15/2021 7:01 AM)
Dear customer,

we can enable qseelogs to uefi by setting EnableQseeLogsFlag@ uefiplat.cfg
+SecurityFlag = 0x1C4

To get TZ logs:

Please add ASSERT_EFI_ERROR(Status) or ASSERT (Status == EFI_SUCCESS) or add any code which will crash device in file you want to debug, then collect dump and check for tz logs.


Thanks,
Padmaneela
Created By: Padmaneela Nallani (7/15/2021 6:51 AM)
Dear customer,

we are looking into your issue and get back soon with required information

Thanks,
Padmaneela