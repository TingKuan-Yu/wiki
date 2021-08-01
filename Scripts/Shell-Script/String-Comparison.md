# How to Check if a String Contains a Substring in Bash
## Using =~
- The result shall be FAIL for below case.
```
echo "Test: fastboot devices"
result=`fastboot devices | grep FAILED`
echo result: $result
if [[ ${result} =~ "FAILED (remote: 'unknown command')" ]]; then
  echo "PASS"
  exit 0
else
  echo "FAILED"
  exit 1
fi
```
## Using Regex Operator 
- reference: https://linuxize.com/post/how-to-check-if-string-contains-substring-in-bash/
- Use the regex operator =~. When this operator is used, the right string is considered as a regular expression. The period followed by an asterisk .* matches zero or more occurrences any character except a newline character.
```
#!/bin/bash

STR='GNU/Linux is an operating system'
SUB='Linux'
 
if [[ "$STR" =~ .*"$SUB".* ]]; then
  echo "It's there."
fi
```
