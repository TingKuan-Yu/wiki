

# About Variables

- references
  - https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_variables?view=powershell-7.1

- Short description
Describes how variables store values that can be used in PowerShell.

- Long description
  - You can store all types of values in PowerShell variables. For example, store the results of commands, and store elements that are used in commands and expressions, such as names, paths, settings, and values.
  - A variable is a unit of memory in which values are stored. In PowerShell, variables are represented by text strings that begin with a dollar sign ($), such as $a, $process, or $my_var.

# Global variable
- The **global** keyword
- example
```
$global:g_dwCreateProcessReturn = 0;
```