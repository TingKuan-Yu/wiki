# CMPT
1. Get Permissions for Source
https://cpmt
2. Make sure you have these:
a. Epsilon -> SWInternal (https://cpmt/member/create/478136/ )
b. MsCoreUEFI -> WorkItem Access and Source Access (https://cpmt/member/create/749286 )
  - need MSCoreUEFI Access Code permission
c. Surface UEFI Common -> Source Access and Surface UEFI Access ¡V Read/Write and WorkItem access (https://cpmt/member/create/763313 )

# Token
a. https://dev.azure.com/e-os/_usersSettings/tokens
Select "New Token"
Name: UEFI Build Access
Organization: All accessible organizations
Scopes:
Code: Read & Write
Packaging: Read
b. Copy pat.txt in working folder (from token)

# ssh public key

7. Installing Azure CLI
a. Information on how to install Azure CLI through APT can be for ?? here ??, but in a nutshell here is what you need to do to install it.
curl -sL https://aka.ms/InstallAzureCLIDeb | sudo bash
az extension add --name azure-devops
b. Login to Azure
a. Run az login to login to Azure.
b. Generate SSH keys
ssh-keygen
c. Once you generate your keys and they are located under ~/.ssh/. Next you need to upload your public SSH key (~/.ssh/id_rsa.pub) to Azure DevOps (for Device and MSFTDEVICE).

# repos
- source
  -  https://dev.azure.com/E-OS/device/_git/SurfaceUEFI
- another method
  - https://dev.azure.com/e-os/device/_wiki/wikis/Wiki/34176/Building-b1-Epsilon-for-Android-11?anchor=building-surface-uefi
   ```
   repo init -u ssh://ssh.dev.azure.com/v3/e-os/device/manifest -b b1/11/main -m nhlos/surfaceuefi.xml
   repo sync
   ```
- build error
```
PROGRESS - ## Syncing Git repositories: MU_BASECORE Common/MSCORE_INTERNAL Common/MU Common/MU_OEM_SAMPLE Common/MU_TIANO Common/SURFACE Common/SURFACE_INTERNAL...
PROGRESS - Done.

PROGRESS - ## Checking Git repository: MU_BASECORE...
ERROR - Failed to fetch MU_BASECORE
```
- required repos
```
url = https://windowspartners.visualstudio.com/MSCoreUEFI/_git/mu_basecore
url = https://windowspartners.visualstudio.com/MSCoreUEFI/_git/Core_UEFI_Internal
url = https://windowspartners.visualstudio.com/MSCoreUEFI/_git/mu_plus
url = https://windowspartners.visualstudio.com/MSCoreUEFI/_git/mu_oem_sample
url = https://windowspartners.visualstudio.com/MSCoreUEFI/_git/mu_tiano_plus
```
- fix sync error
  - **need to apply source access of MSCoreUEFI from CPMT**