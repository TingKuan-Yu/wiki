```
VOID *
GetSocDtb (VOID *Kernel, UINT32 KernelSize, UINT32 DtbOffset, VOID *DtbLoadAddr)
```

```

STATIC EFI_STATUS
ApplyOverlay (BootParamlist *BootParamlistPtr,
              VOID *AppendedDtHdr,
              struct fdt_entry_node *DtsList)
```
- FinalDtbHdr
```
  /* If DeviceTreeLoadAddr == AppendedDtHdr
     CopyMem will not copy Source Buffer to Destination Buffer
     and return Destination BUffer.
  */
  gBS->CopyMem ((VOID *)BootParamlistPtr->DeviceTreeLoadAddr,
                FinalDtbHdr,
                fdt_totalsize (FinalDtbHdr));
```