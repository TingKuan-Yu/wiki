# reference
- https://www.gnu.org/software/make/manual/html_node/Conditional-Functions.html

# if and example, not work now
```
$(if $(and $(),$() ) ), 
  true  ,\
  false  \
) 
```

# skip error when command failed
- reference
  - https://stackoverflow.com/questions/2670130/make-how-to-continue-after-a-command-fails
- example
```
rm file || true

```

# Test Program
- Makefile
```
all:
	@echo "test 1-1"
	$(if $(shell test -s Makefile && echo 1), echo "With Makefile", echo "No Makefile");
	@echo "test 1-2"	
	$(if $(shell test -s Makefile2 && echo 1), echo "With Makefile2", @echo "No Makefile2");
	@echo "test 2-1"
	$(if $(shell test -s Makefile2 && echo 1), echo "With Makefile2", @echo "No Makefile2");
	@echo "test 2-2"	
	$(eval wildcardmakefile := $(wildcard Makefile))
	$(if $(wildcardmakefile), echo "wildcardmakefile:" $(wildcardmakefile), @echo "No localmakefile");
	@echo "test 3-1"
	$(eval wildcardmakefile2 := $(wildcard Makefile2))
	@echo numuber of wildcardmakefile2: $(words $(wildcardmakefile2))	
	$(if $(wildcardmakefile2), echo "wildcardmakefile2: Makefile2", @echo "No wildcardmakefile2");
	@echo "test 3-2"	
	$(eval shelltestmakefile := $(shell test -s Makefile && echo Makefile))
	@echo numuber of shelltestmakefile: $(words $(shelltestmakefile))
	$(if $(shelltestmakefile), echo "shelltestmakefile:" $(shelltestmakefile), @echo "No shelltestmakefile");
	@echo "test 3-3"	
	$(eval shelltestmakefilenum := $(words $(shell test -s Makefile && echo Makefile)) )
	$(if $(shelltestmakefilenum), echo "shelltestmakefilenum:" $(shelltestmakefilenum), @echo "No shelltestmakefilenum");
	@echo "test 4-1"	
	$(eval shelltestmakefilefilter := $(filter $(shell ls Makefile),Makefile) )
	$(if $(shelltestmakefilefilter), echo "shelltestmakefilefilter:" $(shelltestmakefilefilter), @echo "No shelltestmakefilefilter");
	$(eval shelltestmakefilefilter2 := $(filter $(shell ls Makefile2),Makefile2) )
	$(if $(shelltestmakefilefilter2), echo "shelltestmakefilefilter2:" $(shelltestmakefilefilter2), @echo "No shelltestmakefilefilter2");
	@echo "test LS"
	$(eval shellLS := $(shell ls))
	@echo shellLS: $(shellLS)
	test -s Makefile &&  echo "Yes Makefile"
	@echo "test 5-1: eval command"
```