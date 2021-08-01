# cmdlets
 - reference
   - https://whatis.techtarget.com/definition/cmdlet
     - Cmdlets are **.NET classes** written in higher programming languages such as C# and compiled in .dll files so that PowerShell can access them. Thus, cmdlet sets can be easily added and new cmdlets can be created and made available to PowerShell.
 - .NET for ubuntu
   - https://docs.microsoft.com/en-us/dotnet/core/install/linux-snap 

# CmdletBinding
- reference
  - https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_functions_cmdletbindingattribute?view=powershell-7.1
    - The following example shows the format of a function that specifies all the optional arguments of the CmdletBinding attribute. A brief description of each argument follows this example.
    ```
    {
        [CmdletBinding(ConfirmImpact=<String>,
        DefaultParameterSetName=<String>,
        HelpURI=<URI>,
        SupportsPaging=<Boolean>,
        SupportsShouldProcess=<Boolean>,
        PositionalBinding=<Boolean>)]

        Param ($Parameter1)
        Begin{}
        Process{}
        End{}
    }
    ```

# [Parameter(Mandatory=$true)] 
  - Use PowerShell to Make Mandatory Parameters
  - reference
    - https://devblogs.microsoft.com/scripting/use-powershell-to-make-mandatory-parameters/
    - This parameter attribute uses the Parameter keyword, and sets the Mandatory attribute to $true. 

#  [Parameter(Mandatory=$true,Position=0)]
  - reference
    - https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_functions_advanced_parameters?view=powershell-7.1
  - **Mandatory argument**
    The Mandatory argument indicates that the parameter is required. If this argument isn't specified, the parameter is optional.
  - **Position argument**
    - The value of the Position argument is specified as an integer. A position value of 0 represents the first position in the command, a position value of 1 represents the second position in the command, and so on.

# [switch]
 - reference
   - https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_functions_advanced_parameters?view=powershell-7.1
 - To create a switch parameter in a function, specify the Switch type in the parameter definition. For example:
   ```
   Param([Switch]<ParameterName>)

   Param(
       [Parameter(Mandatory=$false)]
       [Switch]
       $<ParameterName>
   )
   ```



  