[[_TOC_]]


# helper link
- https://www.tutorialspoint.com/batch_script/index.htm
- https://www.dostips.com/DtCodeSnippets.php#Snippets.FileSize
- https://www.youtube.com/playlist?list=PL69BE3BF7D0BB69C4


# comments
- https://www.tutorialspoint.com/batch_script/batch_script_comments.htm
- Use below key words for comments.
```
rem I am a annotation.
:: I am a annotation
```

# set variable to current path
```
set current_path=%cd%
```
# for loop
- Microsoft web:
  https://docs.microsoft.com/en-us/windows-server/administration/windows-commands/for
- 


# wmic tool
- Windows Tool wmic
  https://docs.microsoft.com/en-us/windows-server/administration/windows-commands/wmic


```
:: wmic /format:list strips trailing spaces (at least for path win32_pnpentity)
for /f "tokens=1* delims==" %%I in ('wmic path win32_pnpentity Where "Caption LIKE '%%QDLoader%%'" get caption /format:list ^| find "COM"') do (
    call :setCOM "for /f "tokens=1* delims==""
)

:: display all _COM* variables
set _COM > log1.txt

:: end main batch
goto :EOF

:setCOM <WMIC_output_line>
:: sets _COM#=line

set "str=%~1"
set "num=%str:*(COM=%"
set "num=%num:)=%"
set str=%str:(COM=&rem.%
set "_COM%num%=%str%"
```
  