
# Reference
- https://www.ssl.com/how-to/create-a-pfx-p12-certificate-file-using-openssl/#:~:text=The%20PKCS%2312%20or%20PFX%20format%20is%20a%20binary,to%20import%20and%20export%20certificates%20and%20private%20keys.

# pfx introduction
- The PKCS#12 or PFX format is a binary format for storing the server certificate, any intermediate certificates, and the **private key** into a single encryptable file. PFX files are usually found with the extensions .pfx and .p12. PFX files are typically used on Windows and macOS machines to import and export certificates and private keys.

# OEMC1_UEFI_PK_Signer.pfx
- private key for sign blob
- password: ""
  - just press enter is ok

#. Windows Tool
   - certutil -dump <path to cert>
```
C:\VBShare\security\mfg_mode_tool\manufacturing-mode-0.0.13\Certs\OEMC1>certutil -dump OEMC1_UEFI_PK_Signer.pfx
輸入 PFX 密碼:
================ 憑證 0 ================
================  開始巢狀層級 1 ================
元素 0:
序號: 525d434f8a601daa4de21b045c411b25
簽發者: CN=OEMC1 UEFI PK CA, O=Microsoft Corporation, L=Redmond, S=Washington, C=US
 NotBefore: 8/5/2020 12:33 AM
 NotAfter: 8/5/2030 12:43 AM
主體: CN=OEMC1 UEFI PK Signer, O=Microsoft Corporation, L=Redmond, S=Washington, C=US
不是根憑證
Cert 雜湊(sha1): 46097439aa3cffc4d0df5f35129179554626b56f
---------------- 停止巢狀層級 1 ----------------
  提供者 = Microsoft Strong Cryptographic Provider
簽章測試通過
CertUtil: -dump 命令成功完成。
```

# Ubuntu
- openssl pkcs12 -info -in <path to cert> p
```
root@UbuntM-VB:~/security/pck7/mfg_mode_tool/manufacturing-mode-0.0.13/Certs/OEMC1# openssl pkcs12 -info -in OEMC1_UEFI_PK_Signer.pfx
Enter Import Password:
MAC: sha1, Iteration 2000
MAC length: 20, salt length: 20
PKCS7 Data
Shrouded Keybag: pbeWithSHA1And3-KeyTripleDES-CBC, Iteration 2000
Bag Attributes
    Microsoft Local Key set: <No Values>
    localKeyID: 01 00 00 00 
    friendlyName: tq-5ad7d9f1-4e00-4c8d-be67-e2e90e6d58bf
    Microsoft CSP Name: Microsoft Strong Cryptographic Provider
Key Attributes
    X509v3 Key Usage: 80 
Enter PEM pass phrase:
Error outputting keys and certificates
140543217455552:error:28078065:UI routines:UI_set_result_ex:result too small:../crypto/ui/ui_lib.c:903:You must type in 4 to 1024 characters
140543217455552:error:2807106B:UI routines:UI_process:processing error:../crypto/ui/ui_lib.c:543:while reading strings
140543217455552:error:0906406D:PEM routines:PEM_def_callback:problems getting password:../crypto/pem/pem_lib.c:59:
140543217455552:error:0907E06F:PEM routines:do_pk8pkey:read key:../crypto/pem/pem_pk8.c:83:
```
# Ubuntu pfx Operation
## convert pkcs#12 pfx to certificate.pem (Private key + public key)
  - Overview
    PKCS#12 (also known as PKCS12 or PFX) is a common binary format for storing a certificate chain and private key in a single, encryptable file, and usually has the filename extensions .p12 or .pfx. 
  - Conversion
```
tingkuanyu@TonyYuLinux1:/D/c1/security/mfg_win_unlock/Certs$ openssl pkcs12 -in OEMC1_UEFI_PK_Signer.pfx -out certificate.pem -nodes
Enter Import Password:
```

## Convert PEM to CER with DER format
```
tingkuanyu@TonyYuLinux1:/D/c1/security/mfg_win_unlock/Certs$ openssl x509 -outform der -in certificate.pem -out certificate.cer
tingkuanyu@TonyYuLinux1:/D/c1/security/mfg_win_unlock/Certs$ diff certificate.cer OEMC1_UEFI_PK_Signer.cer
```
# verification
```
tingkuanyu@TonyYuLinux1:/D/c1/security/mfg_win_unlock/Certs/test$ openssl cms -verify -in UnsignedBlob.bin.p7 -inform DER -noverify -outform DER -signer ../certificate.pem -out textdata
Verification successful
tingkuanyu@TonyYuLinux1:/D/c1/security/mfg_win_unlock/Certs/test$ diff textdata UnsignedBlob.bin
```