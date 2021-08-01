# Reference
- https://security.stackexchange.com/questions/80410/sign-pkcs7-and-verify-pkcs7-signature-with-openssl

# edk2/CryptoPkg/Library/BaseCryptLib/Pk/CryptPkcs7VerifyCommon.c
## Pkcs7Verify function
```
/**
  Verifies the validity of a PKCS#7 signed data as described in "PKCS #7:
  Cryptographic Message Syntax Standard". The input signed data could be wrapped
  in a ContentInfo structure.

  If P7Data, TrustedCert or InData is NULL, then return FALSE.
  If P7Length, CertLength or DataLength overflow, then return FALSE.

  Caution: This function may receive untrusted input.
  UEFI Authenticated Variable is external input, so this function will do basic
  check for PKCS#7 data structure.

  @param[in]  P7Data       Pointer to the PKCS#7 message to verify.
  @param[in]  P7Length     Length of the PKCS#7 message in bytes.
  @param[in]  TrustedCert  Pointer to a trusted/root certificate encoded in DER, which
                           is used for certificate chain verification.
  @param[in]  CertLength   Length of the trusted certificate in bytes.
  @param[in]  InData       Pointer to the content to be verified.
  @param[in]  DataLength   Length of InData in bytes.

  @retval  TRUE  The specified PKCS#7 signed data is valid.
  @retval  FALSE Invalid PKCS#7 signed data.

**/
BOOLEAN
EFIAPI
Pkcs7Verify (
  IN  CONST UINT8  *P7Data,
  IN  UINTN        P7Length,
  IN  CONST UINT8  *TrustedCert,
  IN  UINTN        CertLength,
  IN  CONST UINT8  *InData,
  IN  UINTN        DataLength
  )

```


# boot/Sm8350FamilyPkg/Library/MsManufacturingModeUtilitiesDxeLib/MsManufacturingModeUtilitiesDxeLib.c
## VerifySignatureAndCertChainWithEku function
- call **Pkcs7Verify**
```
/**
  This function verifies a PKCS#7 formatted signature, and also checks that the
  specified trust anchor is in the signature and that the trust anchor has the
  specified EKUs.

  @param[in] Signature           -- Buffer that holds the PKCS#7 signature.
  @param[in] SizeSignature       -- The number of bytes in Signature.
  @param[in] RootOfTrustCert     -- The root of trust certificate that must
                                    be in the PKCS#7 signature in DER (Binary)
  @param[in] SizeRootOfTrustCert -- The number of bytes in RootOfTrustCert.
  @param[in] EkuString           -- The EKU to check for (optional, can be NULL).
  @param[in] DataToVerify        -- The data to verify.
  @param[in] SizeDataToVerify    -- The number of bytes in DataToVerify.

  @retval EFI_SUCCESS or underlying failure code.
**/
EFI_STATUS
EFIAPI
VerifySignatureAndCertChainWithEku (
  IN CONST UINT8* Signature,
  IN UINTN        SizeSignature,
  IN CONST UINT8* RootOfTrustCert,
  IN UINTN        SizeRootOfTrustCert,
  IN CONST CHAR8* EkuString,
  IN CONST UINT8* DataToVerify,
  IN UINTN        SizeDataToVerify
  )

EFI_STATUS
EFIAPI
IsManufacturingModeEnabled(
  OUT UINT8* IsEnabled
  )
{
:
  DEBUG ((DEBUG_INFO, "[%a] Verifying the signature with Test cert chain DevelopmentPlatformKeyCertificate...\n", __FUNCTION__));
  Status = VerifySignatureAndCertChainWithEku (
             Signature,
             SizeSignature,
             DevelopmentPlatformKeyCertificate,
             DevelopmentSizeOfPlatformKeyCertificate,
             (CONST CHAR8 *)PcdGetPtr (PcdTkRequiredEKU),
             ToBeSignedData,
             SizeToBeSignedData
             );
:
}

```

# required EUK
```
boot/QcomPkg/SocPkg/Lahaina/Common/Core.dsc.inc:
  851    gMsSurfaceCorePkgTokenSpaceGuid.PcdTestMfgModeRequiredEKU|"1.3.6.1.4.1.311.76.9.17"
  852:   gMsSurfaceCorePkgTokenSpaceGuid.PcdTkRequiredEKU|"1.3.6.1.4.1.311.76.9.17"
```

# boot/Sm8350FamilyPkg/Library/PlatformKeyBaseLib/PlatformKeyBaseLib.c
## 
```
#ifndef SHIP_MODE
//
// This certificate is located in:
// Certs/TestCerts/OEMC1_UEFI_PK_SIGNER.cer
// 
CONST UINT8 kaDevelopmentPlatformKeyCertificate[] =
:
:

//
// Test/Development Certificate 
// This is used as for local MFG mode / Debug Mode unlock
//
CONST UINT8 *DevelopmentPlatformKeyCertificate = kaDevelopmentPlatformKeyCertificate;
CONST UINT32 DevelopmentSizeOfPlatformKeyCertificate = sizeof(kaDevelopmentPlatformKeyCertificate);
#endif
```
