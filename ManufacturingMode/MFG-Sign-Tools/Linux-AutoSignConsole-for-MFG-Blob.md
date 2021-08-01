# The AutoSignConsole information from Nirnay
- DevicesWiki - Signing with AutoSign
  - https://www.deviceswiki.com/wiki/Signing_with_AutoSign
  - The document above doesn’t talk about the new parameters required for AutoSign Azure system. ☹ We will get it updated.
- Here is the sample cmdline for your scenario.
```
AutoSignConsole /s -t DbgZeta -b "my business justification" -f "c:\nonce.bin" -path "c:\nonce.bin.p7b" -n “serialNumber” -authType AZDO_JWT -azDOJWTFile C:\token.txt -azDOOrgName E-OS
```
- AutoSignCoonsole Parameters
  - azDOJWTFile
    - parameter expects a token/password that you can get by using [credentialProvider](https://www.nuget.org/packages/Microsoft.VisualStudio.Services.NuGet.CredentialProvider).
    - I usually get the token/password using the following cmdline. 
      - CredentialProvider.VSS.exe -u https://dev.azure.com/E-OS -A

# Get Linux autoconsole tool
- https://dev.azure.com/E-OS/tools/_packaging?_a=package&feed=linux-tools%40Local&package=autosignconsole&version=2.0.1&protocolType=UPack
```
az artifacts universal download --organization "https://dev.azure.com/E-OS/" --feed "linux-tools" --name "autosignconsole" --version "2.0.1" --path .
```

# Steps for create token - Method 1
## 1. Install Visual Studio 2019
- Installation Link
  - https://www.1eswiki.com/wiki/Visual_Studio

## 2. Open Visual Studio to install CredentialProvider
- Reference
  - https://www.nuget.org/packages/Microsoft.VisualStudio.Services.NuGet.CredentialProvider
- A. Use Visual Studio to create a console project
- B. IN Visual Studio, use PM console to execute "Install-Package Microsoft.VisualStudio.Services.NuGet.CredentialProvider -Version 0.37.0".

##  CredentialProvider.VSS.exe -u https://dev.azure.com/E-OS -A
```     
C:\Users\tingkuanyu>cd C:\Users\tingkuanyu\.nuget\packages\microsoft.visualstudio.services.nuget.credentialprovider\0.37.0\tools

CredentialProvider.VSS.exe -u https://dev.azure.com/E-OS -A
```
-output
```
Getting new credentials for https://dev.azure.com/E-OS.
{"__VssPasswordWarning":"WARNING: Treat the authentication token in the password field like a password. Do not share it with anyone, including Microsoft support.","Username":"VssSessionToken","Password":"eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Im9PdmN6NU1fN3AtSGpJS2xGWHo5M3VfVjBabyJ9.eyJuYW1laWQiOiI4MDhkM2NlMi01NGI5LTQ4ZGQtYjk0ZS1iNDIxNDk4NTk4MzgiLCJzY3AiOiJhcHBfdG9rZW4iLCJhdWkiOiJlZTg0NWM3Yy0wYWQyLTQ3ZjUtYWE2MC1jNjlmOGI0NDVlMTUiLCJzaWQiOiJmMDU1OTFkMi0xMjUzLTQ1MWQtYjVhMy0zMGM1MjNhODZlM2IiLCJpc3MiOiJhcHAudnN0b2tlbi52aXN1YWxzdHVkaW8uY29tIiwiYXVkIjoiYXBwLnZzdG9rZW4udmlzdWFsc3R1ZGlvLmNvbXx2c286NzRhNTYyM2YtODIwZi00Nzk4LTg2MDYtMDMzNWFlYzdlYTRlIiwibmJmIjoxNjI2MTU5ODc3LCJleHAiOjE2MjYxNzQ3OTB9.t_0qdZYw_wA_qFTf1Bye5Ivlht6FImFE6pO3XnvCY1uDsv1xGds2--gl-j8wo1t6-AIo9T0CMonZpMK9N5gFhATSK7eWiiTxPRgJucC_2d0PHFsNtRB1TRbXt80ouT10UJ8c5mLw9iYicgO0rT48hYbKjJgdzfIj6DNuHDQaatUbHY6pZ1rPi_ZLNcD0hCijwZZxoIunxTLQWrKT6KqTSWNiDZv5L7NkN1QXNPHgmL-WbfgV4k2ZYVsjsiFg-SwcLiJ5-DqK72bjBV7KCy8-DPPIRJf0nKvqN2nhaJII3ZrEQv6wiYnLMdrxbNgFLQ8eKgPB9spLmH6p5sV3i8vDbQ"}
```
-Password save to azDOJWTFile.txt
```
eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Im9PdmN6NU1fN3AtSGpJS2xGWHo5M3VfVjBabyJ9.eyJuYW1laWQiOiI4MDhkM2NlMi01NGI5LTQ4ZGQtYjk0ZS1iNDIxNDk4NTk4MzgiLCJzY3AiOiJhcHBfdG9rZW4iLCJhdWkiOiJlZTg0NWM3Yy0wYWQyLTQ3ZjUtYWE2MC1jNjlmOGI0NDVlMTUiLCJzaWQiOiJmMDU1OTFkMi0xMjUzLTQ1MWQtYjVhMy0zMGM1MjNhODZlM2IiLCJpc3MiOiJhcHAudnN0b2tlbi52aXN1YWxzdHVkaW8uY29tIiwiYXVkIjoiYXBwLnZzdG9rZW4udmlzdWFsc3R1ZGlvLmNvbXx2c286NzRhNTYyM2YtODIwZi00Nzk4LTg2MDYtMDMzNWFlYzdlYTRlIiwibmJmIjoxNjI2MTU5ODc3LCJleHAiOjE2MjYxNzQ3OTB9.t_0qdZYw_wA_qFTf1Bye5Ivlht6FImFE6pO3XnvCY1uDsv1xGds2--gl-j8wo1t6-AIo9T0CMonZpMK9N5gFhATSK7eWiiTxPRgJucC_2d0PHFsNtRB1TRbXt80ouT10UJ8c5mLw9iYicgO0rT48hYbKjJgdzfIj6DNuHDQaatUbHY6pZ1rPi_ZLNcD0hCijwZZxoIunxTLQWrKT6KqTSWNiDZv5L7NkN1QXNPHgmL-WbfgV4k2ZYVsjsiFg-SwcLiJ5-DqK72bjBV7KCy8-DPPIRJf0nKvqN2nhaJII3ZrEQv6wiYnLMdrxbNgFLQ8eKgPB9spLmH6p5sV3i8vDbQ
```

# Steps for create token - Method 2
•	Get the credential provider. You can download from the nuget.org or you can get from \\desmo\wds\Software\Users\nikhatri\ServiceClient\AutoSignConsole\CredentialProvider
•	Run cmdline:
```
CredentialProvider.VSS.exe -u https://dev.azure.com/E-OS -A
```
•	The above cmdline should print a json string. Copy the value for the password and past in the azDOJWTFile.txt 
•	Call AutoSignConsole.


