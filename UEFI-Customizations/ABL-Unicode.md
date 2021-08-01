# https://dev.azure.com/E-OS/DeviceSW/_workitems/edit/183209?src=WorkItemMention&src-action=artifact_link

# Test

It is good if the oem handle function can pass null point but string length 0 shall be work. I am afraid that make it to null if no parameter could cause other issues.

Accroding to test, no parameter doesn't mean null address. We shall use string length to determine if there is any parameter.
      3. The parameter from fastboot oem command is UNICODE format, so using Ascii functions to covert it before operation is recommended. Please using functions such as AsciiStrCpy,AsciiStrLen, and so on functions in MdePkg/Include/Library/BaseLib.h.


Reference code:
```
VOID CmdOemSetCustomizedKernelParam (CONST CHAR8 *Arg, VOID *Data, UINT32 Size)
{
:
    argumentLen = AsciiStrLen(Arg);
    if (argumentLen <= 1 ) {
        FastbootInfo("\nInvalid argument\n");
    }
```

Test Code:


VOID CmdOemBatteryPPID(CONST CHAR8 *Arg, VOID *Data, UINT32 Size)
{
    EFI_STATUS Status;
    UINTN Len;
    UINT8 WhichPack;
    CHAR8 Buf[32];
    CHAR8 PPID[PPID_LENGTH];
    CHAR8 Res[MAX_RSP_SIZE];

    if(Arg) {
        AsciiSPrint(Res, (UINTN)sizeof(Res), "Arg not null");
        FastbootInfo (Res);
        WaitForTransferComplete ();

        AsciiSPrint(Res, (UINTN)sizeof(Res), "addr Arg: %u", Arg);        
        FastbootInfo (Res);
        WaitForTransferComplete ();

        AsciiSPrint(Res, (UINTN)sizeof(Res), "String Arg: %a", Arg);
        FastbootInfo (Res);
        WaitForTransferComplete ();      

        AsciiSPrint(Res, (UINTN)sizeof(Res), "AsciiStrLen(Arg): %d", AsciiStrLen(Arg));
        FastbootInfo (Res);
        WaitForTransferComplete ();  

    } else {

        AsciiSPrint(Res, (UINTN)sizeof(Res), "Arg is null");
        FastbootInfo (Res);
        WaitForTransferComplete ();
    }


    if(&Arg[0]) {
        AsciiSPrint(Res, (UINTN)sizeof(Res), "&Arg[0] not null");
        FastbootInfo (Res);
        WaitForTransferComplete ();

        AsciiSPrint(Res, (UINTN)sizeof(Res), "addr &Arg[0]: %u", &Arg[0]);        
        FastbootInfo (Res);
        WaitForTransferComplete ();

        AsciiSPrint(Res, (UINTN)sizeof(Res), "String &Arg[0]: %a", &Arg[0]);
        FastbootInfo (Res);
        WaitForTransferComplete ();        

        AsciiSPrint(Res, (UINTN)sizeof(Res), "AsciiStrLen(&Arg[0]): %d", AsciiStrLen(&Arg[0]));
        FastbootInfo (Res);
        WaitForTransferComplete ();  


    } else {

        AsciiSPrint(Res, (UINTN)sizeof(Res), "&Arg[0] is null");
        FastbootInfo (Res);
        WaitForTransferComplete ();
    }

    if(&Arg[1]) {
        AsciiSPrint(Res, (UINTN)sizeof(Res), "&Arg[1] not null");
        FastbootInfo (Res);
        WaitForTransferComplete ();

        AsciiSPrint(Res, (UINTN)sizeof(Res), "addr &Arg[1]: %u", &Arg[1]);        
        FastbootInfo (Res);
        WaitForTransferComplete ();

        AsciiSPrint(Res, (UINTN)sizeof(Res), "String &Arg[1]: %a", &Arg[1]);
        FastbootInfo (Res);
        WaitForTransferComplete ();        

        AsciiSPrint(Res, (UINTN)sizeof(Res), "AsciiStrLen(&Arg[1]): %d", AsciiStrLen(&Arg[1]));
        FastbootInfo (Res);
        WaitForTransferComplete ();  

    } else {

        AsciiSPrint(Res, (UINTN)sizeof(Res), "&Arg[1] is null");
        FastbootInfo (Res);
        WaitForTransferComplete ();
    }

    if(&Arg[2]) {
        AsciiSPrint(Res, (UINTN)sizeof(Res), "&Arg[2] not null");
        FastbootInfo (Res);
        WaitForTransferComplete ();

        AsciiSPrint(Res, (UINTN)sizeof(Res), "addr &Arg[2]: %u", &Arg[2]);        
        FastbootInfo (Res);
        WaitForTransferComplete ();

        AsciiSPrint(Res, (UINTN)sizeof(Res), "String &Arg[2]: %a", &Arg[2]);
        FastbootInfo (Res);
        WaitForTransferComplete ();  

        AsciiSPrint(Res, (UINTN)sizeof(Res), "AsciiStrLen(&Arg[2]): %d", AsciiStrLen(&Arg[2]));
        FastbootInfo (Res);
        WaitForTransferComplete ();

    } else {

        AsciiSPrint(Res, (UINTN)sizeof(Res), "&Arg[2] is null");
        FastbootInfo (Res);
        WaitForTransferComplete ();
    }

    FastbootOkay ("");
    return ;


}


Result:

tingkuanyu@TonyYuLinux1:/D/c1/11/main/abl$ fastboot oem battery-ppid
(bootloader) Arg not null
(bootloader) addr Arg: 2611068944
(bootloader) String Arg:
(bootloader) AsciiStrLen(Arg): 0
(bootloader) &Arg[0] not null
(bootloader) addr &Arg[0]: 2611068944
(bootloader) String &Arg[0]:
(bootloader) AsciiStrLen(&Arg[0]): 0
(bootloader) &Arg[1] not null
(bootloader) addr &Arg[1]: 2611068945
(bootloader) String &Arg[1]:
(bootloader) AsciiStrLen(&Arg[1]): 0
(bootloader) &Arg[2] not null
(bootloader) addr &Arg[2]: 2611068946
(bootloader) String &Arg[2]:
(bootloader) AsciiStrLen(&Arg[2]): 0
OKAY [  0.001s]
Finished. Total time: 0.001s
tingkuanyu@TonyYuLinux1:/D/c1/11/main/abl$ fastboot oem battery-ppid 123
(bootloader) Arg not null
(bootloader) addr Arg: 2611068944
(bootloader) String Arg:  123
(bootloader) AsciiStrLen(Arg): 4
(bootloader) &Arg[0] not null
(bootloader) addr &Arg[0]: 2611068944
(bootloader) String &Arg[0]:  123
(bootloader) AsciiStrLen(&Arg[0]): 4
(bootloader) &Arg[1] not null
(bootloader) addr &Arg[1]: 2611068945
(bootloader) String &Arg[1]: 123
(bootloader) AsciiStrLen(&Arg[1]): 3
(bootloader) &Arg[2] not null
(bootloader) addr &Arg[2]: 2611068946
(bootloader) String &Arg[2]: 23
(bootloader) AsciiStrLen(&Arg[2]): 2
OKAY [  0.001s]
Finished. Total time: 0.001s
tingkuanyu@TonyYuLinux1:/D/c1/11/main/abl$ fastboot oem battery-ppid
(bootloader) Arg not null
(bootloader) addr Arg: 2611068944
(bootloader) String Arg:
(bootloader) AsciiStrLen(Arg): 0
(bootloader) &Arg[0] not null
(bootloader) addr &Arg[0]: 2611068944
(bootloader) String &Arg[0]:
(bootloader) AsciiStrLen(&Arg[0]): 0
(bootloader) &Arg[1] not null
(bootloader) addr &Arg[1]: 2611068945
(bootloader) String &Arg[1]: 123
(bootloader) AsciiStrLen(&Arg[1]): 3
(bootloader) &Arg[2] not null
(bootloader) addr &Arg[2]: 2611068946
(bootloader) String &Arg[2]: 23
(bootloader) AsciiStrLen(&Arg[2]): 2
OKAY [  0.001s]
Finished. Total time: 0.001s
tingkuanyu@TonyYuLinux1:/D/c1/11/main/abl$ fastboot oem battery-ppid 12345
(bootloader) Arg not null
(bootloader) addr Arg: 2611068944
(bootloader) String Arg:  12345
(bootloader) AsciiStrLen(Arg): 6
(bootloader) &Arg[0] not null
(bootloader) addr &Arg[0]: 2611068944
(bootloader) String &Arg[0]:  12345
(bootloader) AsciiStrLen(&Arg[0]): 6
(bootloader) &Arg[1] not null
(bootloader) addr &Arg[1]: 2611068945
(bootloader) String &Arg[1]: 12345
(bootloader) AsciiStrLen(&Arg[1]): 5
(bootloader) &Arg[2] not null
(bootloader) addr &Arg[2]: 2611068946
(bootloader) String &Arg[2]: 2345
(bootloader) AsciiStrLen(&Arg[2]): 4
OKAY [  0.001s]
Finished. Total time: 0.001s