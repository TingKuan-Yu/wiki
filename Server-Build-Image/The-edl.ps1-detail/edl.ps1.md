# The edl.ps1 explaination

## Header comments
- script snippet
```
#-------------------------------------------------------------------------------
# Copyright (c) Microsoft Corporation.  All rights reserved.
#-------------------------------------------------------------------------------
<#
.SYNOPSIS
    Contact Scott Fudally (sfudally@microsoft.com) for any changes needed to this script

.PARAMETER None
    None
#>
#Requires -Version 5.0
```
- purposes or functions
  - show copyright and version
- \# or <# #>
  - The # and <# #> can be used for block comments and more specifically for help comments.


## Parameters of edl.ps1
- script snippet
```
[CmdletBinding()]
param(
 [Parameter(Mandatory=$true,Position=0)]
 [string] $EDL_Action,
 [Parameter(Mandatory=$false,Position=1)]
 [int] $ComPort = -1,
 [Parameter(Mandatory=$false,Position=2)]
 [string] $DumpPath,
 [Parameter(Mandatory=$false)]
 [int] $ResetTimeOut = 10,
 [Parameter(Mandatory=$false)]
 [switch] $SuppressRedScreen
)
```
- purposes or functions
  - specific required and optional parameters of edl.ps1
  - The first parameter is necessary with a string parameter value. The value will be save into EDL_Action.
  - Other parameters are optional.






# The Whole Script
[edl.ps1](/.attachments/edl-c605b535-8a60-4b16-830b-bdb0e97c0746.ps1)