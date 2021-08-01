# bootable/bootloader/edk2/QcomModulePkg/Library/avb/VerifiedBoot.c
- set AllowVerificationError to TRUE
- force GREEN from ORANGE
```
STATIC EFI_STATUS
LoadImageAndAuthVB2 (BootInfo *Info)
{
:
  BOOLEAN AllowVerificationError = TRUE;//Skip verification: IsUnlocked (); 

  if (AllowVerificationError) {
    //force GREEN from ORANGE: Info->BootState = ORANGE;
    Info->BootState = GREEN;
  } else {
    if (UserData->IsUserKey) {
      Info->BootState = YELLOW;
    } else {
      Info->BootState = GREEN;
    }
  }

```

- add code to skip verification
```
STATIC EFI_STATUS LoadImageAndAuthForLE (BootInfo *Info)
{

    DEBUG ((EFI_D_INFO, "VB: verification skipped for debug builds\n"));
    goto skip_verification;

```
- force AVB_SLOT_VERIFY_RESULT_OK
# bootable/bootloader/edk2/QcomModulePkg/Library/avb/libavb/avb_slot_verify.c
```

  if (avb_safe_memcmp(digest, desc_digest, digest_len) != 0) {
    avb_errorv(part_name,
               ": Hash of data does not match digest in descriptor.\n",
               NULL);
    // force AVB_SLOT_VERIFY_RESULT_OK: ret = AVB_SLOT_VERIFY_RESULT_ERROR_VERIFICATION;
    ret = AVB_SLOT_VERIFY_RESULT_OK;
    goto out;
  } else {
    avb_debugv (part_name, ": success: Image verification completed\n", NULL);
  }

  ret = AVB_SLOT_VERIFY_RESULT_OK;

```