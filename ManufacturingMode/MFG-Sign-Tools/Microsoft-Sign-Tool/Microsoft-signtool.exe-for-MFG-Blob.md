# Website
- https://docs.microsoft.com/zh-tw/dotnet/framework/tools/signtool-exe

# Usage
signtool.exe" sign /debug 
/p7 C:\VBShare\security\mfg_mode_tool\manufacturing-mode-0.0.13 
/fd sha256 
/p7co 1.2.840.113549.1.7.1 
/f "C:\VBShare\security\mfg_mode_tool\manufacturing-mode-0.0.13\Certs\OEMC1\OEMC1_UEFI_PK_SIGNER.pfx" 
/p ""  
/ac "C:\VBShare\security\mfg_mode_tool\manufacturing-mode-0.0.13\Certs\OEMC1\OEMC1_UEFI_PK_CA.cer" 
/u 1.3.6.1.4.1.311.76.9.17

# Used parameter
## /debug 
- Display additional debug information.
## /p7 C:\VBShare\security\mfg_mode_tool\manufacturing-mode-0.0.13
- /p7 <path>: Specifies that for each specified content file a pkcs7 file is
              produced. The pkcs7 file will be named: <path>\<file>.p7
## /fd sha256 
- /fd         Specifies the file digest algorithm to use for creating file
            signatures. (Default is SHA1)

## /p7co 1.2.840.113549.1.7.1 
- /p7co <OID>   Specifies the <OID> that identifies the signed content.

## /f "C:\VBShare\security\mfg_mode_tool\manufacturing-mode-0.0.13\Certs\OEMC1\OEMC1_UEFI_PK_SIGNER.pfx" 
- /f <file>   Specify the signing cert in a file. If this file is a **PFX with
            a password**, the password may be supplied with the "/p" option.
            If the file does not contain private keys, use the "/csp" and "/kc"
            options to specify the CSP and container name of the private key.

## /p "" 
- /p <pass.>  Specify a password to use when opening the PFX file.

## /ac "C:\VBShare\security\mfg_mode_tool\manufacturing-mode-0.0.13\Certs\OEMC1\OEMC1_UEFI_PK_CA.cer" 
- /ac <file>  Add an additional certificate, from <file>, to the signature block.

## /u 1.3.6.1.4.1.311.76.9.17
- /u <usage>  Specify the **Enhanced Key Usage (EKU)** that must be present in the cert.
            The parameter may be specified by **OID** or by string. The default
            usage is "Code Signing" (1.3.6.1.5.5.7.3.3).

# Sing Help
```

PS C:\VBShare\security\mfg_mode_tool\manufacturing-mode-0.0.13\x86> .\signtool.exe sign /?
Usage: signtool sign [options] <filename(s)>

Use the "sign" command to sign files using embedded signatures. Signing
protects a file from tampering, and allows users to verify the signer (you)
based on a signing certificate. The options below allow you to specify signing
parameters and to select the signing certificate you wish to use.

Certificate selection options:
/a          Select the best signing cert automatically. SignTool will find all
            valid certs that satisfy all specified conditions and select the
            one that is valid for the longest. If this option is not present,
            SignTool will expect to find only one valid signing cert.
/ac <file>  Add an additional certificate, from <file>, to the signature block.
/c <name>   Specify the Certificate Template Name (Microsoft extension) of the
            signing cert.
/f <file>   Specify the signing cert in a file. If this file is a PFX with
            a password, the password may be supplied with the "/p" option.
            If the file does not contain private keys, use the "/csp" and "/kc"
            options to specify the CSP and container name of the private key.
/i <name>   Specify the Issuer of the signing cert, or a substring.
/n <name>   Specify the Subject Name of the signing cert, or a substring.
/p <pass.>  Specify a password to use when opening the PFX file.
/r <name>   Specify the Subject Name of a Root cert that the signing cert must
            chain to.
/s <name>   Specify the Store to open when searching for the cert. The default
            is the "MY" Store.
/sm         Open a Machine store instead of a User store.
/sha1 <h>   Specify the SHA1 thumbprint of the signing cert.
/fd         Specifies the file digest algorithm to use for creating file
            signatures. (Default is SHA1)
/u <usage>  Specify the Enhanced Key Usage that must be present in the cert.
            The parameter may be specified by OID or by string. The default
            usage is "Code Signing" (1.3.6.1.5.5.7.3.3).
/uw         Specify usage of "Windows System Component Verification"
            (1.3.6.1.4.1.311.10.3.6).

Private Key selection options:
/csp <name> Specify the CSP containing the Private Key Container.
/kc <name>  Specify the Key Container Name of the Private Key.

Signing parameter options:
/as         Append this signature. If no primary signature is present, this
            signature will be made the primary signature instead.
/d <desc.>  Provide a description of the signed content.
/du <URL>   Provide a URL with more information about the signed content.
/t <URL>    Specify the timestamp server's URL. If this option is not present,
            the signed file will not be timestamped. A warning is generated if
            timestamping fails.
/tr <URL>   Specifies the RFC 3161 timestamp server's URL. If this option
            (or /t) is not specified, the signed file will not be timestamped.
            A warning is generated if timestamping fails.  This switch cannot
            be used with the /t switch.
/tseal <URL> Specifies the RFC 3161 timestamp server's URL for timestamping a
            sealed file.
/td <alg>   Used with the /tr or /tseal switch to request a digest algorithm
            used by the RFC 3161 timestamp server.
/seal       Add a sealing signature if the file format supports it.
/itos       Create a primary signature with the intent-to-seal attribute.
/force      Continue to seal or sign in situations where the existing signature
            or sealing signature needs to be removed to support sealing.
/nosealwarn Sealing-related warnings do not affect SignTool's return code.

PKCS7 options:
/p7 <path>    Specifies that for each specified content file a pkcs7 file is
              produced. The pkcs7 file will be named: <path>\<file>.p7
/p7co <OID>   Specifies the <OID> that identifies the signed content.
/p7ce <Value> Defined values:
                Embedded           - Embeds the signed content in the pkcs7.
                DetachedSignedData - Produces the signed data part of
                                     a detached pkcs7.
              The default is 'Embedded'

Other options:
/ph         Generate page hashes for executable files if supported.
/nph        Suppress page hashes for executable files if supported.
            The default is determined by the SIGNTOOL_PAGE_HASHES
            environment variable and by the wintrust.dll version.
/q          No output on success and minimal output on failure. As always,
            SignTool returns 0 on success, 1 on failure, and 2 on warning.
/v          Print verbose success and status messages. This may also provide
            slightly more information on error.
/debug      Display additional debug information.
```