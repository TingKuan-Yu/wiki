# Build command
---
## ./build.sh build_boot
- build xbl, xbl_config, shrm and other images
## ./build.sh clean_boot
- clean all build artifacts

# build.sh
---
## shell script
```
## ./build.sh clean_boot
```

## important definition

- shell global variable AZURE_DEVOPS_EXT_PAT
  - Needed to be defined in .bashrc. Such as the following example.
```
export AZURE_DEVOPS_EXT_PAT=jjodvbk..........................gzhqiqy6adz2ks7rkdq
```

- TARGET="lahaina"
  - target platform of xbl

- parameter -fetch
  - The FETCH then be set to y
  - Then, call docker env to make getpkg_nhlo
     ```
     docker run $DOCKERINTERACTIVE -t --mount type=bind,source=$SCRIPTPATH,target=/s -w=/s $RUNUSERID -e AZURE_DEVOPS_EXT_PAT "$IMAGE_REPO/$PKG_IMAGE_PATH" -c "make getpkg_nhlos" 
     ```   
   - The "make getpkg_nhlos" use Makefile (Makefile -> scripts/Makefile --> includes scripts/makefile.main.mk) to make **getpkg_nhlos** 

- build_command
  - build_command="make TARGET=${TARGET} $MAXCPU $1"
  - $1: build_boot or clean_boot

## make method
- use docker and build_command to do makeing
```
echo "> Building nhlos via docker"
echo "   - build_command: $build_command"
if [ -z "$BAREDOCKER" ]; then
  docker run $DOCKERINTERACTIVE -t --mount type=bind,source=$SCRIPTPATH,target=/s -w=/s $RUNUSERID -e AZBUILDVER -e AZBUILDVERINT "$IMAGE_REPO/$IMAGE_PATH" -c "$build_command"
else
  echo "   - Launching Docker Build environment only"
  docker run -it --mount type=bind,source=$SCRIPTPATH,target=/s -w=/s $RUNUSERID -e AZBUILDVER -e AZBUILDVERINT "$IMAGE_REPO/$IMAGE_PATH" -c "/bin/bash"
fi
```

# Makefile
---
- .repo/manifests/projects/projects-nhlos-device.xml
```
  <!-- This file contains links to the Devices' specific tools for NHLOS content -->
  <!-- nhlos build scripts -->
  <project remote="device" groups="eos,device" name="device/nhlos-build-scripts" path="scripts">
    <linkfile dest="Makefile" src="Makefile"/>
    <linkfile dest="build.sh" src="build.sh"/>
    <linkfile dest="artifactcopy.py" src="artifactcopy.py"/>
  </project>
```
- This Makefile simply includes scripts/makefile.main.mk

# scripts/makefile.main.mk
---
## target **getpkg_nhlos**
- call gekpgs.py with packages-release.json to get artificats
```
getpkg_nhlos: test_eos_build
	python3.6 $(ROOT_DIR)/eos_build/scripts/getpkgs.py -p $(ROOT_DIR)/artifacts/nhlos/packages-release.json -r $(ROOT_DIR)

test_eos_build:
	@test -d $(ROOT_DIR)/eos_build || { echo "ERROR ERROR ERROR: Steps aren't available - eos_build is not included"; false; }
```
## target to build boot images
- clean_boot
```
clean_boot: test_boot
	export SECTOOLS_DIR=$(META_DIR)/sectools;\
	cd $(BOOT_PKG_DIR) && \
		python buildex.py -t Lahaina,QcomToolsPkg -v LAA -r RELEASE -b cleanall
```
- build_boot
```
build_boot: test_boot tools
	export SECTOOLS_DIR=$(META_DIR)/sectools;\
	cd $(BOOT_PKG_DIR) && \
		python buildex.py -t Lahaina,QcomToolsPkg -v LAA -r RELEASE
```
- build_boot_ship
```
# MS_CHANGE, Enable SHIP_MODE
build_boot_ship: test_boot tools
	export SECTOOLS_DIR=$(META_DIR)/sectools;\
	cd $(BOOT_PKG_DIR) && \
		python buildex.py -t Lahaina,QcomToolsPkg -v LAA -r RELEASE "-c -DSHIP_MODE -DUSER_BUILD_VARIANT"
```
- clean_boot_debug
```
clean_boot_debug: test_boot
	export SECTOOLS_DIR=$(META_DIR)/sectools;\
	cd $(BOOT_PKG_DIR) && \
		python buildex.py -t Lahaina,QcomToolsPkg -v LAA -r DEBUG -b cleanall
```
- build_boot_debug
```
build_boot_debug: test_boot tools
	cd $(BOOT_PKG_DIR) && \
		python buildex.py -t Lahaina,QcomToolsPkg -v LAA -r DEBUG
```

# ./artifacts/nhlos/packages-release.json
---
## for fetching c1-11-main-component
```
    "defaults": {
        "organization": "https://dev.azure.com/E-OS",
        "feed": "c1-11-main-component",
        "version": "*",
        "path": ".",
        "project": null,
        "hashCheck": true,
        "wipepath": false,
        "filter": []
    },
    "packages": [
        {
            "name": "adsp-release"
        },
    :
```




