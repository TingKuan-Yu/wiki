# The edl.sh explaination

## using /bin/bash
- script snippet
```
#!/bin/bash
```
- purposes or functions
  - This script use /bin/bash as shell program.

## define MY_PATH
- script snippet
```
MY_PATH="`dirname \"$0\"`"
```
- purposes or functions
  - find the directory or path of current script
- script explanation
  - $0
    - expands to the name of the shell or shell script.
  - dirname
    - The dirname command in Linux prints a file path with its final component removed.
    - example
      ```
      tony@tony-ST50:/android/zeta/images$ dirname c1-11-developer-edl-2021.429.8/edl.sh 
      c1-11-developer-edl-2021.429.8
      ``` 
  - MY_PATH
    - It indicate the file directory of edl.sh


## define FHLOADERBIN
- script snippet
```
FHLOADERBIN="./fh_loader/fh_loader.bin"
```
- purposes or functions
  - Set the related path name of fh_loader.bin to edl.sh
  - for chmod +x only
- fh_loader stands for fire hose loader.
  - It is use to communicate with firehose program in the target.

## define QSAHARASRVBIN
- script snippet
```
QSAHARASRVBIN="./fh_loader/QSaharaServer.bin"
```
- purposes or functions
  - Set the related path name of QSaharaServer.bin to edl.sh
  - for chmod +x only
- QSaharaServer is use to communicate with target by sahara protocol.



## Check if powershell is installed
- script snippet
```
#check if powershell is installed
if [ -z "$(which pwsh)" ]; then
    echo ""
    echo "Please install powershell for Linux"
    echo "https://docs.microsoft.com/en-us/powershell/scripting/install/installing-powershell-core-on-linux?view=powershell-6#ubuntu-1804"
    echo ""
    exit 1
fi
```
- purposes or functions
  - if powershell is not installed, ask user to install.


## change mode of FHLOADERBIN and QSAHARASRVBIN for execution
- script snippet
```
if [ ! -x "${FHLOADERBIN}" ]; then
    chmod +x  ${FHLOADERBIN}
fi

if [ ! -x "${QSAHARASRVBIN}" ]; then
    chmod +x  ${QSAHARASRVBIN}
fi
```


## Ask user to stop ModemManager
- script snippet
```
PS_RESULT=$(ps ax | grep [M]odemManager)
if [[ "$PS_RESULT" != "" ]];then
    echo ""
    echo "WARNING: ModemManager is running and may interfere with serial port access."
    echo "Use \"sudo systemctl stop ModemManager\" to shut it down."
    echo ""
    sleep 4
fi
```
- purposes or functions
  -  avoid downloading failed
- systemctl 
  - Linux tool
  - Control the systemd system and service manager
  - us "sudo systemctl stop" to stop system daemon


## invoke edl.ps1 flash script
- script snippet
```
#invoke powershell flash script
$(which pwsh) -NoLogo -NoProfile -ExecutionPolicy Bypass -Command "${MY_PATH}/edl.ps1 $@"
```
- purposes or functions
  - use edl.ps1 to download images
- which pwsh
   ```
   tony@tony-ST50:/android/zeta/c1/11/kernel$ which pwsh
   /usr/bin/pwsh
   ```
- powershell parameters
  - -NoLogo
    Hides the copyright banner at startup.
  - -NoProfile
    Does not load the PowerShell profile.
  - -ExecutionPolicy <ExecutionPolicy>
    Sets the default execution policy for the current session and saves it in the     $env:PSExecutionPolicyPreference environment variable. This parameter does not change     the PowerShell execution policy that is set in the registry. For information about     PowerShell execution policies, including a list of valid values, see     about_Execution_Policies.
    - Bypass. Nothing is blocked and there are no warnings or prompts.
  - -Command
Executes the specified commands (and any parameters) as though they were typed at the PowerShell command prompt, and then exits, unless the NoExit parameter is specified.
    - ${MY_PATH}/edl.ps1 $@
      - $@ is all of the parameters passed to the script from Linux shell





# The whole code of edl.sh 
```
#!/bin/bash

MY_PATH="`dirname \"$0\"`"
FHLOADERBIN="./fh_loader/fh_loader.bin"
QSAHARASRVBIN="./fh_loader/QSaharaServer.bin"

#check if powershell is installed
if [ -z "$(which pwsh)" ]; then
    echo ""
    echo "Please install powershell for Linux"
    echo "https://docs.microsoft.com/en-us/powershell/scripting/install/installing-powershell-core-on-linux?view=powershell-6#ubuntu-1804"
    echo ""
    exit 1
fi

if [ ! -x "${FHLOADERBIN}" ]; then
    chmod +x  ${FHLOADERBIN}
fi

if [ ! -x "${QSAHARASRVBIN}" ]; then
    chmod +x  ${QSAHARASRVBIN}
fi

PS_RESULT=$(ps ax | grep [M]odemManager)
if [[ "$PS_RESULT" != "" ]];then
    echo ""
    echo "WARNING: ModemManager is running and may interfere with serial port access."
    echo "Use \"sudo systemctl stop ModemManager\" to shut it down."
    echo ""
    sleep 4
fi

#invoke powershell flash script
$(which pwsh) -NoLogo -NoProfile -ExecutionPolicy Bypass -Command "${MY_PATH}/edl.ps1 $@"
```