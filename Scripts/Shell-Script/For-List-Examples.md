[[_TOC_]]

# references
- https://www.tutorialspoint.com/unix/unix-using-arrays.htm


# ls to array and the use for loop to print out
```
#!/bin/bash

array=($(ls -1 *.txt))
for element in "${array[@]}"
do
echo ${element}
done
```