# call SignAndUnlockZeta.cmd
```
C:\VBShare\security\mfg_mode_tool\manufacturing-mode-0.0.13>UnlockZetaWithTestCerts.cmd

C:\VBShare\security\mfg_mode_tool\manufacturing-mode-0.0.13>call SignAndUnlockZeta.cmd -Mode "Test"
Using Test certificate chain...
```
# C:\windows\system32\CertUtil.exe
```
C:\windows\system32\CertUtil.exe -f -p "" -sid 22 -importPFX My "C:\VBShare\security\mfg_mode_tool\manufacturing-mode-0.0.13\Certs\OEMC1\OEMC1_UEFI_PK_SIGNER.pfx"
True
stdout: 您必須有系統管理員權限，才能使用選取的選項。請使用系統管理員命令提示字元來完成這些工作。
CertUtil: 存取被拒。

exit code: -2147024891
CreateProcess : Process C:\windows\system32\CertUtil.exefailed with exit code: 0x80070005
位於 C:\VBShare\security\mfg_mode_tool\manufacturing-mode-0.0.13\SignAndUnlockZeta.ps1:286 字元:5
+     CreateProcess $szCertUtilPath $szArgs
+     ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : NotSpecified: (:) [Write-Error], WriteErrorException
    + FullyQualifiedErrorId : Microsoft.PowerShell.Commands.WriteErrorException,CreateProcess


C:\windows\system32\CertUtil.exe -silent -user -f -p ""  -importPFX  My "C:\VBShare\security\mfg_mode_tool\manufacturing-mode-0.0.13\Certs\OEMC1\OEMC1_UEFI_PK_SIGNER.pfx"
True
stdout: 憑證 "OEMC1 UEFI PK Signer" 已新增到存放區中。


exit code: 0

Import-Certificate : 存取被拒。 (Exception from HRESULT: 0x80070005 (E_ACCESSDENIED))
位於 線路:1 字元:1
+ Import-Certificate -CertStoreLocation Cert:\LocalMachine\Root -FilePa ...
+ ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : NotSpecified: (:) [Import-Certificate], UnauthorizedAccessException
    + FullyQualifiedErrorId : System.UnauthorizedAccessException,Microsoft.CertificateServices.Commands.ImportCertific
   ateCommand

Import-Certificate : 存取被拒。 (Exception from HRESULT: 0x80070005 (E_ACCESSDENIED))
位於 線路:1 字元:1
+ Import-Certificate -CertStoreLocation Cert:\LocalMachine\CA -FilePath ...
+ ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : NotSpecified: (:) [Import-Certificate], UnauthorizedAccessException
    + FullyQualifiedErrorId : System.UnauthorizedAccessException,Microsoft.CertificateServices.Commands.ImportCertific
   ateCommand
```

# fastboot.exe "oem" "get-mfg-blob"
```
Executing GetBlob with: C:\VBShare\security\mfg_mode_tool\manufacturing-mode-0.0.13\x86\platform-tools\fastboot.exe "oem" "get-mfg-blob"
C:\VBShare\security\mfg_mode_tool\manufacturing-mode-0.0.13\x86\platform-tools\fastboot.exe "oem" "get-mfg-blob"
stdout:
stderr:                                                    (bootloader) SIGNATURE SALT BEGIN --->

(bootloader) C0002DF4457376F506DCC7DCC2E1C324
(bootloader) D8086872C5EDBF191AAF83DC8637AE8B
(bootloader) <--- SIGNATURE SALT END

OKAY [  0.003s]
Finished. Total time: 0.003s

exit code: 0



C0002DF4457376F506DCC7DCC2E1C324
C0002DF4457376F506DCC7DCC2E1C324D8086872C5EDBF191AAF83DC8637AE8B
C0002DF4457376F506DCC7DCC2E1C324D8086872C5EDBF191AAF83DC8637AE8B
C0002DF4457376F506DCC7DCC2E1C324D8086872C5EDBF191AAF83DC8637AE8B
C0002DF4457376F506DCC7DCC2E1C324D8086872C5EDBF191AAF83DC8637AE8B
C0002DF4457376F506DCC7DCC2E1C324D8086872C5EDBF191AAF83DC8637AE8B
C0002DF4457376F506DCC7DCC2E1C324D8086872C5EDBF191AAF83DC8637AE8B
192 0 45 244 69 115 118 245 6 220 199 220 194 225 195 36 216 8 104 114 197 237 191 25 26 175 131 220 134 55 174 139
```
# signtool.exe with **OEMC1_UEFI_PK_SIGNER.pfx**, **OEMC1_UEFI_PK_CA.cer** and **EUK**
- signtool.exe sign /debug 
/p7 C:\VBShare\security\mfg_mode_tool\manufacturing-mode-0.0.13 
/fd sha256 
/p7co 1.2.840.113549.1.7.1 
/f "C:\VBShare\security\mfg_mode_tool\manufacturing-mode-0.0.13\Certs\OEMC1\OEMC1_UEFI_PK_SIGNER.pfx" 
/p ""  
/ac "C:\VBShare\security\mfg_mode_tool\manufacturing-mode-0.0.13\Certs\OEMC1\OEMC1_UEFI_PK_CA.cer" 
/u 1.3.6.1.4.1.311.76.9.17 
C:\VBShare\security\mfg_mode_tool\manufacturing-mode-0.0.13\UnsignedBlob.bin
```
"C:\VBShare\security\mfg_mode_tool\manufacturing-mode-0.0.13\x86\signtool.exe" sign /debug /p7 C:\VBShare\security\mfg_mode_tool\manufacturing-mode-0.0.13 /fd sha256 /p7co 1.2.840.113549.1.7.1 /f "C:\VBShare\security\mfg_mode_tool\manufacturing-mode-0.0.13\Certs\OEMC1\OEMC1_UEFI_PK_SIGNER.pfx" /p ""  /ac "C:\VBShare\security\mfg_mode_tool\manufacturing-mode-0.0.13\Certs\OEMC1\OEMC1_UEFI_PK_CA.cer" /u 1.3.6.1.4.1.311.76.9.17 C:\VBShare\security\mfg_mode_tool\manufacturing-mode-0.0.13\UnsignedBlob.bin
True
stdout:
The following certificates were considered:
    Issued to: OEMC1 UEFI PK Signer
    Issued by: OEMC1 UEFI PK CA
    Expires:   Mon Aug 05 00:43:06 2030
    SHA1 hash: 46097439AA3CFFC4D0DF5F35129179554626B56F

After EKU filter, 1 certs were left.
After expiry filter, 1 certs were left.
After Private Key filter, 1 certs were left.
The following certificate was selected:
    Issued to: OEMC1 UEFI PK Signer
    Issued by: OEMC1 UEFI PK CA
    Expires:   Mon Aug 05 00:43:06 2030
    SHA1 hash: 46097439AA3CFFC4D0DF5F35129179554626B56F

Cross certificate chain (using machine store) (Partial):
    Issued to: OEMC1 UEFI PK CA
    Issued by: OEMC1 Third Party Marketplace Root
    Expires:   Sun Aug 05 00:42:42 2040
    SHA1 hash: 1C75C86B916ABB67BDA9A2F23C973D8B320D3C45

        Issued to: OEMC1 UEFI PK Signer
        Issued by: OEMC1 UEFI PK CA
        Expires:   Mon Aug 05 00:43:06 2030
        SHA1 hash: 46097439AA3CFFC4D0DF5F35129179554626B56F


The following additional certificates will be attached:
Done Adding Additional Store
Successfully signed: C:\VBShare\security\mfg_mode_tool\manufacturing-mode-0.0.13\UnsignedBlob.bin

Number of files successfully Signed: 1
Number of warnings: 0
Number of errors: 0

exit code: 0
```
# fastboot.exe "flash" "set-mfg-blob" 
```
Executing signature provisioning tool with: C:\VBShare\security\mfg_mode_tool\manufacturing-mode-0.0.13\x86\platform-tools\fastboot.exe "flash" "set-mfg-blob" "C:\VBShare\security\mfg_mode_tool\manufacturing-mode-0.0.13\UnsignedBlob.bin.p7"C:\VBShare\security\mfg_mode_tool\manufacturing-mode-0.0.13\x86\platform-tools\fastboot.exe "flash" "set-mfg-blob" "C:\VBShare\security\mfg_mode_tool\manufacturing-mode-0.0.13\UnsignedBlob.bin.p7"
True
stdout:
stderr: Sending 'set-mfg-blob' (1 KB)                      OKAY [  0.007s]
Writing 'set-mfg-blob'                             OKAY [  0.008s]
Finished. Total time: 0.027s

exit code: 0
Sending 'set-mfg-blob' (1 KB)                      OKAY [  0.007s]
Writing 'set-mfg-blob'                             OKAY [  0.008s]
Finished. Total time: 0.027s

Clearing userdata: C:\VBShare\security\mfg_mode_tool\manufacturing-mode-0.0.13\x86\platform-tools\fastboot.exe "erase" "userdata"
C:\VBShare\security\mfg_mode_tool\manufacturing-mode-0.0.13\x86\platform-tools\fastboot.exe "erase" "userdata"
True
stdout:
stderr: ******** Did you mean to fastboot format this f2fs partition?
Erasing 'userdata'                                 OKAY [  0.099s]
Finished. Total time: 0.112s

exit code: 0
******** Did you mean to fastboot format this f2fs partition?
Erasing 'userdata'                                 OKAY [  0.099s]
Finished. Total time: 0.112s

Clearing metadata: C:\VBShare\security\mfg_mode_tool\manufacturing-mode-0.0.13\x86\platform-tools\fastboot.exe "erase" "metadata"
C:\VBShare\security\mfg_mode_tool\manufacturing-mode-0.0.13\x86\platform-tools\fastboot.exe "erase" "metadata"
True
stdout:
stderr: Erasing 'metadata'                                 OKAY [  0.079s]
Finished. Total time: 0.092s

exit code: 0
Erasing 'metadata'                                 OKAY [  0.079s]
Finished. Total time: 0.092s

------------------------------------------------------
Successfully placed the device into MANUFACTURING_MODE
Need reboot to enter MANUFACTURING_MODE
------------------------------------------------------

Reboot now? (Y/N): y

Executing reboot: "C:\VBShare\security\mfg_mode_tool\manufacturing-mode-0.0.13\x86\platform-tools\fastboot.exe" "reboot""C:\VBShare\security\mfg_mode_tool\manufacturing-mode-0.0.13\x86\platform-tools\fastboot.exe" "reboot"
True
stdout:
stderr: Rebooting                                          OKAY [  0.001s]
Finished. Total time: 0.001s

exit code: 0
Rebooting                                          OKAY [  0.001s]
```