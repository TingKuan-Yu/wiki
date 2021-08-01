-lsmod
```
c1:/ # lsmod | grep -i bt                                                                                                                                                                                    
bt_fm_slim             32768  1 
btpower                36864  1 bt_fm_slim
```

- code in abl
  - note: device unbootable
```

EFI_STATUS
PrintAsciiBuffer (char *PrintStr, unsigned length)
{
  #define MAX_PRINT_BUFFER 128
  char PrintBuffer[MAX_PRINT_BUFFER];
  
  if(length >= (MAX_PRINT_BUFFER - 1)) {
    DEBUG ((DEBUG_ERROR, "[%a] - Invalid input length.\n", __FUNCTION__));
    return EFI_INVALID_PARAMETER;
  }

  if(!PrintStr) {
    DEBUG ((DEBUG_ERROR, "[%a] - Invalid input string.\n", __FUNCTION__));
    return EFI_INVALID_PARAMETER;
  }

  //AsciiStrnCpy (PrintBuffer, PrintStr, length);
  memcpy (PrintBuffer, PrintStr, length);
  PrintBuffer[length] = 0;
  //DEBUG ((DEBUG_INFO, "[%a] - PrintStr: %a\n", __FUNCTION__,PrintStr));
  DEBUG ((DEBUG_INFO, "[%a] - PrintStr: %a\n", __FUNCTION__,PrintBuffer));

  return EFI_SUCCESS;

}


char* strsearch(char* targetstring, unsigned int strlen, const char* needle) {
  size_t n, m;

  for (n = 0; n<strlen; n++) {
    if (targetstring[n] != needle[0]) {
      continue;
    }

    for (m = 1;; m++) {
      if (needle[m] == '\0') {
        return targetstring + n;
      }

      if (targetstring[n + m] != needle[m]) {
        break;
      }
    }
  }

  return NULL;
}

EFI_STATUS
RenameStrFirstLetterWithUnderline(char **RenameStr, unsigned int strsize, const char *Pattern)
{
  char* pSearchStr = *RenameStr;
  char* pMatchedStr;
  unsigned int PatternLen = strlen(Pattern);
  unsigned int leftlen = strsize;

  if(!RenameStr) {
    DEBUG ((DEBUG_ERROR, "[%a] - Invalid RenameStr.\n", __FUNCTION__));
    return EFI_INVALID_PARAMETER;
  }

  DEBUG ((EFI_D_INFO, "Replace with Pattern: %a, len: %d \n", Pattern,PatternLen));

  while(leftlen > 0) {
    //pMatchedStr = AsciiStrStr(pSearchStr, Pattern);
    pMatchedStr = strsearch(pSearchStr,leftlen, Pattern);
    //PrintAsciiBuffer(pMatchedStr,PatternLen);

    if(pMatchedStr) {
      //pMatchedStr[0] = '_';
      *pMatchedStr = '_';
      DEBUG ((EFI_D_INFO, "Replaced string: "));
      PrintAsciiBuffer(pMatchedStr,PatternLen);
      DEBUG ((EFI_D_INFO, "\n"));
      leftlen = leftlen - (pMatchedStr - pSearchStr);
      pSearchStr = pMatchedStr + 1;
    } else {
      DEBUG ((EFI_D_INFO, "No more %a string found.\n",Pattern));
      DEBUG ((EFI_D_INFO, "\n"));      
      return EFI_SUCCESS;
    }
  }
  
  return EFI_SUCCESS;
}


 // Tony: @todo: replace compatible name
  /* If DeviceTreeLoadAddr == AppendedDtHdr
     CopyMem will not copy Source Buffer to Destination Buffer
     and return Destination BUffer.
  */
  RenameStrFirstLetterWithUnderline((char **)&BootParamlistPtr->DeviceTreeLoadAddr, DT_SIZE_2MB, "btfmslim_slave");


```