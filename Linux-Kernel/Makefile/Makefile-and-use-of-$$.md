#Makefile and use of $$
- https://stackoverflow.com/questions/19589957/makefile-and-use-of
- http://pubs.opengroup.org/onlinepubs/9699919799/utilities/make.html
```
Make needs to distinguish whether you want a $ to use as introducing a make-variable reference, such as ${FOOBAR} or as a plain $ passed on to the shell. The make specification (Section Macros) says that to do the latter, you must use $$ which is replaced by a single $ and passed to the shell. In effect, your snippet reads as

for file_exe in `find . -name "zip_exe-*"`; do \
   ./${file_exe} -d some/unzip/path/lib; \
done
to the shell.

Style note: Iterating over file lists created by backticks is considered bad style, since it may overflow the ARG_MAX limit. Better to read the file names one-by-one with

find . -name "zip_exe-*" | \
while read -r file_exe; do \
   ./${file_exe} -d some/unzip/path/lib; \
done

```