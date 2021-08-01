# call .ps1 file in powershell
- not allow to call directly
```
PS C:\Users\tingkuanyu\OneDrive - Microsoft\TechStudy\PowerShell> function.ps1
function.ps1 : The term 'function.ps1' is not recognized as the name of a cmdlet, function, script file, or operable program. Check the spelling of the name, or if a
path was included, verify that the path is correct and try again.
At line:1 char:1
+ function.ps1
+ ~~~~~~~~~~~~
    + CategoryInfo          : ObjectNotFound: (function.ps1:String) [], CommandNotFoundException
    + FullyQualifiedErrorId : CommandNotFoundException
```


# ExecutionPolicy

- reference
  - https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.security/get-executionpolicy?view=powershell-7.1
  - https://www.netspi.com/blog/technical/network-penetration-testing/15-ways-to-bypass-the-powershell-execution-policy/

- Get-ExecutionPolicy
```
PS C:\Users\tingkuanyu> Get-ExecutionPolicy
Restricted
```

# call .ps1 file with bypass ExecutionPolicy
- without bypass
```
PS C:\Users\tingkuanyu\OneDrive - Microsoft\TechStudy\PowerShell> powershell -file .\function.ps1
File C:\Users\tingkuanyu\OneDrive - Microsoft\TechStudy\PowerShell\function.ps1 cannot be loaded because running scripts is disabled on this system. For more
information, see about_Execution_Policies at https:/go.microsoft.com/fwlink/?LinkID=135170.
    + CategoryInfo          : SecurityError: (:) [], ParentContainsErrorRecordException
    + FullyQualifiedErrorId : UnauthorizedAccess
```
- with bypass
```
PS C:\Users\tingkuanyu\OneDrive - Microsoft\TechStudy\PowerShell> powershell -ExecutionPolicy bypass -file .\function.ps1
```

