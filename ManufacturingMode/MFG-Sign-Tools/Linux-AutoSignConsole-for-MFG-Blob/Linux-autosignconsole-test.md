# 1. Connect Linux VPN
```
tingkuanyu@TonyYuLinux1:~/bin$ ./start.sh
```

# 2. sign blob test
- ./AutoSignConsole /s -t DbgZeta -b "my business justification" -f "./UnsignedBlob.bin" -path "./UnsignedBlob.bin.p7b" -n "serialNumber" -authType AZDO_JWT -azDOJWTFile ./azDOJWTFile.txt -azDOOrgName E-OS
```
tingkuanyu@TonyYuLinux1:/D/c1/security/autosignconsole/2.0.1$ ./AutoSignConsole /s -t DbgZeta -b "my business justification" -f "./UnsignedBlob.bin" -path "./UnsignedBlob.bin.p7b" -n "serialNumber" -authType AZDO_JWT -azDOJWTFile ./azDOJWTFile.txt -azDOOrgName E-OS
5/13/2021 1:13:21 AM AutoSignConsole 1.24.137.0
5/13/2021 1:13:21 AM Signing Type = DbgZeta
5/13/2021 1:13:21 AM Serial Number = serialNumber
5/13/2021 1:13:21 AM Business Justification = my business justification
5/13/2021 1:13:21 AM Submit File = UnsignedBlob.bin
5/13/2021 1:13:21 AM Submit File Size = 32 bytes
5/13/2021 1:13:21 AM Signature File Path = ./UnsignedBlob.bin.p7b
5/13/2021 1:13:21 AM AuthType = AZDO_JWT
5/13/2021 1:13:21 AM Azure Dev Ops Org Name for Auth = E-OS
5/13/2021 1:13:25 AM RequestId = 194894
5/13/2021 1:13:25 AM UploadFileAsync for requestId 194894; Attempt # 1
5/13/2021 1:13:25 AM Bytes uploaded: 0
5/13/2021 1:13:25 AM Bytes uploaded: 0
5/13/2021 1:13:25 AM Bytes uploaded: 0
5/13/2021 1:13:25 AM Bytes uploaded: 0
5/13/2021 1:13:27 AM Bytes uploaded: 32
5/13/2021 1:13:27 AM Bytes uploaded: 32
5/13/2021 1:13:31 AM Waiting for the request to be approved.

5/13/2021 1:14:38 AM Exit Code = 6
ERROR! Message: System.ApplicationException: Request failed signing. RequestId: 194894. Info Message: One or more errors occurred.System.ArgumentException: Unable to map tingkuanyu@microsoft.com to DOMAIN\alias string
   at Microsoft.Surface.AutoSign.AutoSignSigningAgent.Util.ActiveDirectoryDomainNameUtility.GetDomainAliasNameFromEmail(String adMemberEmailAddress) in C:\w\519\s\AutoSignSigningAgent\Utils\ActiveDirectoryDomainNameUtility.cs:line 54
   at Microsoft.Surface.AutoSign.AutoSignSigningAgent.SignRequestWorker.UpdateRequestorIfIsEmail(IRequest request) in C:\w\519\s\AutoSignSigningAgent\SignRequestWorker.cs:line 324
   at Microsoft.Surface.AutoSign.AutoSignSigningAgent.RetryTaskHandler.Try[T1](Action`1 action, T1 arg1, Int32 retryCount, Int32 retryIntervalInMilliseconds, HashSet`1 exceptionsThatAreNotRetrieable) in C:\w\519\s\AutoSignSigningAgent\RetryTaskHandler.cs:line 87
System.ArgumentException: Unable to map tingkuanyu@microsoft.com to DOMAIN\alias string
   at Microsoft.Surface.AutoSign.AutoSignSigningAgent.Util.ActiveDirectoryDomainNameUtility.GetDomainAliasNameFromEmail(String adMemberEmailAddress) in C:\w\519\s\AutoSignSigningAgent\Utils\ActiveDirectoryDomainNameUtility.cs:line 54
   at Microsoft.Surface.AutoSign.AutoSignSigningAgent.SignRequestWorker.UpdateRequestorIfIsEmail(IRequest request) in C:\w\519\s\AutoSignSigningAgent\SignRequestWorker.cs:line 324
   at Microsoft.Surface.AutoSign.AutoSignSigningAgent.RetryTaskHandler.Try[T1](Action`1 action, T1 arg1, Int32 retryCount, Int32 retryIntervalInMilliseconds, HashSet`1 exceptionsThatAreNotRetrieable) in C:\w\519\s\AutoSignSigningAgent\RetryTaskHandler.cs:line 87
System.ArgumentException: Unable to map tingkuanyu@microsoft.com to DOMAIN\alias string
   at Microsoft.Surface.AutoSign.AutoSignSigningAgent.Util.ActiveDirectoryDomainNameUtility.GetDomainAliasNameFromEmail(String adMemberEmailAddress) in C:\w\519\s\AutoSignSigningAgent\Utils\ActiveDirectoryDomainNameUtility.cs:line 54
   at Microsoft.Surface.AutoSign.AutoSignSigningAgent.SignRequestWorker.UpdateRequestorIfIsEmail(IRequest request) in C:\w\519\s\AutoSignSigningAgent\SignRequestWorker.cs:line 324
   at Microsoft.Surface.AutoSign.AutoSignSigningAgent.RetryTaskHandler.Try[T1](Action`1 action, T1 arg1, Int32 retryCount, Int32 retryIntervalInMilliseconds, HashSet`1 exceptionsThatAreNotRetrieable) in C:\w\519\s\AutoSignSigningAgent\RetryTaskHandler.cs:line 87
System.ArgumentException: Unable to map tingkuanyu@microsoft.com to DOMAIN\alias string
   at Microsoft.Surface.AutoSign.AutoSignSigningAgent.Util.ActiveDirectoryDomainNameUtility.GetDomainAliasNameFromEmail(String adMemberEmailAddress) in C:\w\519\s\AutoSignSigningAgent\Utils\ActiveDirectoryDomainNameUtility.cs:line 54
   at Microsoft.Surface.AutoSign.AutoSignSigningAgent.SignRequestWorker.UpdateRequestorIfIsEmail(IRequest request) in C:\w\519\s\AutoSignSigningAgent\SignRequestWorker.cs:line 324
   at Microsoft.Surface.AutoSign.AutoSignSigningAgent.RetryTaskHandler.Try[T1](Action`1 action, T1 arg1, Int32 retryCount, Int32 retryIntervalInMilliseconds, HashSet`1 exceptionsThatAreNotRetrieable) in C:\w\519\s\AutoSignSigningAgent\RetryTaskHandler.cs:line 87
System.ArgumentException: Unable to map tingkuanyu@microsoft.com to DOMAIN\alias string
   at Microsoft.Surface.AutoSign.AutoSignSigningAgent.Util.ActiveDirectoryDomainNameUtility.GetDomainAliasNameFromEmail(String adMemberEmailAddress) in C:\w\519\s\AutoSignSigningAgent\Utils\ActiveDirectoryDomainNameUtility.cs:line 54
   at Microsoft.Surface.AutoSign.AutoSignSigningAgent.SignRequestWorker.UpdateRequestorIfIsEmail(IRequest request) in C:\w\519\s\AutoSignSigningAgent\SignRequestWorker.cs:line 324
   at Microsoft.Surface.AutoSign.AutoSignSigningAgent.RetryTaskHandler.Try[T1](Action`1 action, T1 arg1, Int32 retryCount, Int32 retryIntervalInMilliseconds, HashSet`1 exceptionsThatAreNotRetrieable) in C:\w\519\s\AutoSignSigningAgent\RetryTaskHandler.cs:line 87

   at Microsoft.Devices.Security.AutoSign.WebClient.RequestSearcher.GetRequestResult(Int64 requestId, IList`1 outputPaths, AutoSignConsoleSettings settings) in C:\w\164\s\AutoSignConsole\RequestSearcher\RequestSearcher.cs:line 89
   at Microsoft.Devices.Security.AutoSign.WebClient.AutoSignConsole.GetResult(Int64 requestId, IList`1 outputPaths, AutoSignConsoleSettings settings) in C:\w\164\s\AutoSignConsole\AutoSignConsole.cs:line 161
   at Microsoft.Devices.Security.AutoSign.WebClient.Program.Main(String[] args) in C:\w\164\s\AutoSignConsole\Program.cs:line 89

```