# bootable/bootloader/edk2/QcomModulePkg/Library/FastbootLib/FastbootCmds.c
- CmdOemSelectDisplayPanel (CONST CHAR8 *arg, VOID *data, UINT32 sz)
```
    Status = DisplayGetVariable ((CHAR16 *)L"DisplayPanelOverride",
                                 (VOID *)DisplayPanelStrExist,
                                 &CurStrLen);

      AsciiStrnCatS (DisplayPanelStr,
                     MAX_DISPLAY_PANEL_OVERRIDE,
                     DisplayPanelStrExist,
                     CurStrLen);

  AsciiStrnCatS (DisplayPanelStr,
                 MAX_DISPLAY_PANEL_OVERRIDE,
                 arg,
                 AsciiStrLen (arg));

  /* Update the environment variable with the selected panel */
  Status = DisplaySetVariable ((CHAR16 *)L"DisplayPanelOverride",
                               (VOID *)DisplayPanelStr,
                               AsciiStrLen (DisplayPanelStr));

```

# QC Doc
- KBA-180302023415
