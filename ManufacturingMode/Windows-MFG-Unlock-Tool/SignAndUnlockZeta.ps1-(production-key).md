
# Key execution log

## Executing GetBlob with: C:\VBShare\security\mfg_mode_tool\manufacturing-mode-0.0.13\x86\platform-tools\fastboot.exe "oem" "get-mfg-blob"
```
C:\VBShare\security\mfg_mode_tool\manufacturing-mode-0.0.13\x86\platform-tools\fastboot.exe "oem" "get-mfg-blob"
stdout:
stderr:                                                    (bootloader) SIGNATURE SALT BEGIN --->

(bootloader) 8E4F37C2166762E3ECB24341E3EFCA8D
(bootloader) 066429515E44CA8398731114EA8E83C1
(bootloader) <--- SIGNATURE SALT END

OKAY [  0.000s]
Finished. Total time: 0.000s

exit code: 0
```
## Executing signing proxy tool with: C:\VBShare\security\mfg_mode_tool\manufacturing-mode-0.0.13\x86\SurfaceSigningProxyClient.exe DbgZeta C:\VBShare\security\mfg_mode_tool\manufacturing-mode-0.0.13\UnsignedBlob.bin
```
This is production signing, takes ~10 seconds to finish, sit back and relax...
C:\VBShare\security\mfg_mode_tool\manufacturing-mode-0.0.13\x86\SurfaceSigningProxyClient.exe DbgZeta C:\VBShare\security\mfg_mode_tool\manufacturing-mode-0.0.13\UnsignedBlob.bin
True
stdout: SurfaceSigningProxyClient

exit code: 0
```

## Executing signature provisioning tool with: C:\VBShare\security\mfg_mode_tool\manufacturing-mode-0.0.13\x86\platform-tools\fastboot.exe "flash" "set-mfg-blob" "C:\VBShare\security\mfg_mode_tool\manufacturing-mode-0.0.13\UnsignedBlob.bin.p7b"
```
C:\VBShare\security\mfg_mode_tool\manufacturing-mode-0.0.13\x86\platform-tools\fastboot.exe "flash" "set-mfg-blob" "C:\VBShare\security\mfg_mode_tool\manufacturing-mode-0.0.13\UnsignedBlob.bin.p7b"
True
stdout:
stderr: Sending 'set-mfg-blob' (2 KB)                      OKAY [  0.000s]
Writing 'set-mfg-blob'                             OKAY [  0.000s]
Finished. Total time: 0.016s

exit code: 0
Sending 'set-mfg-blob' (2 KB)                      OKAY [  0.000s]
Writing 'set-mfg-blob'                             OKAY [  0.000s]
Finished. Total time: 0.016s
```






