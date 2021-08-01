
# The %~dp0 Variable
- https://stackoverflow.com/questions/5034076/what-does-dp0-mean-and-how-does-it-work
  - The %~dp0 (that’s a zero) variable when referenced within a Windows batch file will expand to the drive letter and path of that batch file.
  - The variables **%0-%9 refer to the command line parameters of the batch file**. %1-%9 refer to command line arguments after the batch file name. %0 refers to the batch file itself.
- call_cmd.cmd
```
echo "%~dp0"
call variable_test.cmd %*
```
- variable_test.cmd
```
echo "%~dpn0" %*
pushd "%~dp0"
echo "%~dpn0" %*
popd
```
- C:\Users\tingkuanyu\OneDrive - Microsoft\TechStudy\DosCmd>call_cmd.cmd
  - use call the %dp0 includes the name of the callee such as variable_test
```
C:\Users\tingkuanyu\OneDrive - Microsoft\TechStudy\DosCmd>echo "C:\Users\tingkuanyu\OneDrive - Microsoft\TechStudy\DosCmd\"
"C:\Users\tingkuanyu\OneDrive - Microsoft\TechStudy\DosCmd\"

C:\Users\tingkuanyu\OneDrive - Microsoft\TechStudy\DosCmd>call variable_test.cmd

C:\Users\tingkuanyu\OneDrive - Microsoft\TechStudy\DosCmd>echo "C:\Users\tingkuanyu\OneDrive - Microsoft\TechStudy\DosCmd\variable_test"
"C:\Users\tingkuanyu\OneDrive - Microsoft\TechStudy\DosCmd\variable_test"

C:\Users\tingkuanyu\OneDrive - Microsoft\TechStudy\DosCmd>pushd "C:\Users\tingkuanyu\OneDrive - Microsoft\TechStudy\DosCmd\"

C:\Users\tingkuanyu\OneDrive - Microsoft\TechStudy\DosCmd>echo "C:\Users\tingkuanyu\OneDrive - Microsoft\TechStudy\DosCmd\variable_test"
"C:\Users\tingkuanyu\OneDrive - Microsoft\TechStudy\DosCmd\variable_test"

C:\Users\tingkuanyu\OneDrive - Microsoft\TechStudy\DosCmd>popd

```

# The %* Variable
- script
```
echo "%*"
```
- test 
```
C:\Users\tingkuanyu\OneDrive - Microsoft\TechStudy\DosCmd>echo "test test2"
"test test2"

C:\Users\tingkuanyu\OneDrive - Microsoft\TechStudy\DosCmd>variable_test.cmd test

C:\Users\tingkuanyu\OneDrive - Microsoft\TechStudy\DosCmd>echo "test"
"test"
```