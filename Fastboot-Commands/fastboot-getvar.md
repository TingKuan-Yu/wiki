[[_TOC_]]

# Overview
This page shows some useful variables which can be got by "fastboot getvar" command.

# Secure variables

- ## fastboot getvar secure
  - FastbootPublishVar ("secure", IsSecureBootEnabled () ? "yes" : "no");
  - IsSecureBootEnabled ()
    - call to is_secure_device() function in QcomPkg/Drivers/VerifiedBootDxe/scm_util.c of boot.
    - If any of the QFPROM is blown, return true.
 ```
  if ( !CHECK_BIT(secure_state, SECBOOT_FUSE )                &&
       !CHECK_BIT(secure_state, SHK_FUSE )                    &&
       !CHECK_BIT(secure_state, RPMB_ENABLED_FUSE )           &&
       !CHECK_BIT(secure_state, TZ_INV_NONINV_DEBUG_FUSE  )   &&
       !CHECK_BIT(secure_state, MSS_INV_NONINV_DEBUG_FUSE )   &&
       !CHECK_BIT(secure_state, CP_INV_NONINV_DEBUG_FUSE  )   && 
       !CHECK_BIT(secure_state, NS_INV_DEBUG_FUSE  )    )
  {
    *is_secure = TRUE;
  }

```
