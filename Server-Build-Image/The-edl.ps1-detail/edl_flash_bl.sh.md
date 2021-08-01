# The edl_flash_bl.sh explaination

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

## define EDL_ACTION
- script snippet
```
EDL_ACTION=`basename $0 .sh|tr '-' '_'`
```
- purposes or functions
  - find the edl of from the name of shell script
- script explanation
  - $0
    - Expands to the name of the shell or shell script.
    - For this script, it is **edl_flash_bl.sh**.
  - basename is a command-line utility that strips directory and trailing suffix from given file names.
    - The following example shows how to use the basename command inside a bash for loop to rename all files ending with “.jpeg” in the current directory by replacing the file extension from “.jpeg” to “.jpg”:
      ```
      for file in *.jpeg; do
          mv -- "$file" "$(basename $file .jpeg).jpg"
      done
      ```

- EDL_ACTION
  - For this script, the EDL_ACTION eauqls **edl_flash_bl**.


## invoke edl.sh
- script snippet
```
bash ${MY_PATH}/edl.sh ${EDL_ACTION} $@
```
- purposes or functions
  - Invoke edl.sh with ${EDL_ACTION} and parameters($@) from edl_flash_bl.sh
- example instance
  - **./edl.sh edl_flash_bl**


# The edl_flash_bl.sh source
```
#!/bin/bash

MY_PATH="`dirname \"$0\"`"
EDL_ACTION=`basename $0 .sh|tr '-' '_'`
bash ${MY_PATH}/edl.sh ${EDL_ACTION} $@
```
