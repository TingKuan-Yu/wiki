# About Functions Advanced Parameters

## Static parameter
- Static parameters are parameters that are always available in the function. Most parameters in PowerShell cmdlets and scripts are static parameters.
- The following example shows the declaration of a ComputerName parameter that has the following characteristics:
  - It's mandatory (required).
  - It takes input from the pipeline.
  - It takes an array of strings as input.
```
Param(
    [Parameter(Mandatory=$true,
    ValueFromPipeline=$true)]
    [String[]]
    $ComputerName
)
```
- function_param.ps1
```
function Print-Dbg {

	Param(
    [Parameter(Mandatory=$true,
    ValueFromPipeline=$true)]
    [String] $printoutmsg
	)
	
	Write-Host $printoutmsg
}
```

# About Functions CmdletBindingAttribute

- reference
  - https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_functions_cmdletbindingattribute?view=powershell-7.1
  - https://www.itprotoday.com/powershell/what-does-powershells-cmdletbinding-do

- Short description
Describes the attribute that makes a function work like a compiled cmdlet.

- Long description
  - The CmdletBinding attribute is an attribute of functions that makes them operate like compiled cmdlets written in C#. It provides access to the features of cmdlets.
  - PowerShell binds the parameters of functions that have the CmdletBinding attribute in the same way that it binds the parameters of compiled cmdlets.
  - It's not unusual to see folks write PowerShell scripts and functions whose first line is [CmdletBinding()]. What's it do? It's generally a big part of advanced functions, or what some folks call "script cmdlets." Basically, it turns on cmdlet-style parameter binding capabilities, either for a script or for a function. 

