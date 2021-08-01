# Reference
- https://docs.microsoft.com/en-us/powershell/scripting/learn/ps101/09-functions?view=powershell-7.1


# A simple function
- A function in PowerShell is declared with the function keyword followed by the function name and then an open and closing curly brace. The code that the function will execute is contained within those curly braces.
```
function Get-Version {
    $PSVersionTable.PSVersion
}
```
- function.ps1
```
function Get-Version {
    $PSVersionTable.PSVersion
}
```

# call function Get-Version
- Get-Version
- test function.ps1
```
PS C:\Users\tingkuanyu\OneDrive - Microsoft\TechStudy\PowerShell> powershell -ExecutionPolicy bypass -file .\function.ps1

Major  Minor  Build  Revision
-----  -----  -----  --------
5      1      19041  906
```


# call function Get-Version
```
Print-Dbg "Hello"
```
- call function_param.ps1
```
PS C:\Users\tingkuanyu\OneDrive - Microsoft\TechStudy\PowerShell>  powershell -ExecutionPolicy bypass -file .\function_param.ps1
Hello
```





