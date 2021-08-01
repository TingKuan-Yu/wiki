# $PSVersionTable
```
PS /E/debug_tools/logcapture> $PSVersionTable

Name                           Value
----                           -----
PSVersion                      7.1.3
PSEdition                      Core
GitCommitId                    7.1.3
OS                             Linux 5.4.0-77-generic #86-Ubuntu SMP Thu Jun 17 02:35:03 UTC 2021
Platform                       Unix
PSCompatibleVersions           {1.0, 2.0, 3.0, 4.0…}
PSRemotingProtocolVersion      2.3
SerializationVersion           1.1.0.1
WSManStackVersion              3.0
```

# Trap
- https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_trap?view=powershell-7.1
```
trap {
    Write-Output "----- TRAP ----"
    Write-Output "Unhandled Exception: $($_.Exception.GetType().Name)"
    Write-Output $_.Exception
    $_ | Format-List -Force
    exit 9988
}
```

# $PSScriptRoot
```
PS /E/debug_tools/logcapture> Get-ChildItem -Path $PSScriptRoot

    Directory: /E/debug_tools/logcapture

Mode                 LastWriteTime         Length Name
----                 -------------         ------ ----
-----           7/12/2021  5:15 PM           1080 logcapture.ps1
-----           7/12/2021  4:32 PM             65 logcapture.sh
-----           7/12/2021  4:31 PM            912 mpbr.ps1
```

# Get-Date
```
PS /E/debug_tools/logcapture> Get-Date -Format "dddd MM/dd/yyyy HH:mm K"
Monday 07/12/2021 17:22 +08:00

PS /E/debug_tools/logcapture> Get-Date -Format "MM_dd_yy_HHmm"
07_12_21_1723

PS /E/debug_tools/logcapture> Get-Date -UFormat "%d%B%Y_%H%M"
12July2021_1730
```

# ConvertFrom-Json
```
PS /E/debug_tools/SurfaceLogTaker> Get-Content -Raw -Path ./LogTakerSetup.json | ConvertFrom-Json

getprop getprop_z logcat dmesg
------- --------- ------ -----
      1         0      1     0

PS /E/debug_tools/SurfaceLogTaker> cat ./LogTakerSetup.json                                      
{
    "getprop": 1,
    "getprop_z": 0,
    "logcat": 1,
    "dmesg": 0
}
```

# comparsion
- https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_comparison_operators?view=powershell-7.1
```
2 -eq 2                 # Output: True
2 -eq 3                 # Output: False
"abc" -eq "abc"         # Output: True
"abc" -eq "abc", "def"  # Output: False
"abc" -ne "def"         # Output: True
"abc" -ne "abc"         # Output: False
"abc" -ne "abc", "def"  # Output: True
```

