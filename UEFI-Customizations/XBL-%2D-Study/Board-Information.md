# ABL

## Library/BootLib/Board.c:
- 

````
STATIC struct BoardInfo platform_board_info;

 
 EFI_STATUS BoardInit (VOID)
 {
   EFI_STATUS Status;
   EFIChipInfoModemType ModemType;
   UINT32 DdrType;
 
   Status = GetChipInfo (&platform_board_info, &ModemType);
   if (EFI_ERROR (Status))
      return Status;
  
   Status = GetPlatformInfo (&platform_board_info);
   if (EFI_ERROR (Status))
      return Status;
```