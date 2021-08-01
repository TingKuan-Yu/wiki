- change command line
```
EFI_STATUS
ReplaceStrConsoleTo_onsole(CHAR8 **FinalCmdLine)
{
  CHAR8* MatchedStr = *FinalCmdLine;

  while(MatchedStr) {
    MatchedStr = AsciiStrStr(MatchedStr, "console=");

    if(MatchedStr) {
      //AsciiStrnCpyS (MatchedStr, AsciiStrLen (MatchedStr), "_", AsciiStrLen ("_"));
      MatchedStr[0] = '_';
      DEBUG ((EFI_D_INFO, "replaced command line: %a \n", MatchedStr));
      DEBUG ((EFI_D_INFO, "\n"));
      MatchedStr++;
    } else {
      DEBUG ((EFI_D_INFO, "The console= string was not found.\n"));
      DEBUG ((EFI_D_INFO, "\n"));      
      return EFI_SUCCESS;
    }
  }
  
  return EFI_SUCCESS;
}
```

- vendor/qcom/proprietary/devicetree/qcom/lahaina.dtsi
```
	chosen {
		bootargs = "log_buf_len=256K earlycon=msm_geni_serial,0x98c000 rcupdate.rcu_expedited=1 rcu_nocbs=0-7 kpti=off";
	};
```

- kernel/msm-5.4/drivers/tty/serial/earlycon.c:227: early_param("earlycon", param_setup_earlycon);
```
/* early_param wrapper for setup_earlycon() */
static int __init param_setup_earlycon(char *buf)
{
	int err;

        // @todo

	/* Just 'earlycon' is a valid param for devicetree and ACPI SPCR. */
	if (!buf || !buf[0]) {
		if (IS_ENABLED(CONFIG_ACPI_SPCR_TABLE)) {
			earlycon_acpi_spcr_enable = true;
			return 0;
		} else if (!buf) {
			return early_init_dt_scan_chosen_stdout();
		}
	}

	err = setup_earlycon(buf);
	if (err == -ENOENT || err == -EALREADY)
		return 0;
	return err;
}
early_param("earlycon", param_setup_earlycon);
```