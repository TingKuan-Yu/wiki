[[_TOC_]]

# The build.sh of ABL & XBL


# Script Analysis

## Bash Declaration

```
#!/bin/bash
```
  - The **#!/bin/bash** means
    - This script is a bash script

## SCRIPTPATH
```
SCRIPTPATH=`cd "$( dirname "${BASH_SOURCE[0]}" )" >/dev/null 2>&1 && pwd`
```
  - **${BASH_SOURCE[0]}**:  the first parameter of bash script
     - For build.sh, it is **build.sh**.

  - **dirname**: strip last component from file name
    ```
    tony@tony-ST50:/android/zeta/c1/11/abl$ dirname build.sh 
    .
    tony@tony-ST50:/$ dirname /android/zeta/c1/11/abl/build.sh 
    /android/zeta/c1/11/abl
    ```
  - The expression **$(command)** is a modern synonym for **`command`** which stands for command substitution; it means run command and put its output here.
    ```
    tony@tony-ST50:/$ echo $(dirname /android/zeta/c1/11/abl/build.sh)
    /android/zeta/c1/11/abl
   
    tony@tony-ST50:/$ cd $(dirname /android/zeta/c1/11/abl/build.sh)
    tony@tony-ST50:/android/zeta/c1/11/abl$
    ```
  - the ">/dev/null 2>&1": echo any error to /dev/null
  - &&: lets you do something based on whether the previous command completed successfully - that's why you tend to see it chained as do_something && do_something_else_that_depended_on_something.
  - pwd: print name of current/working directory
  - **SCRIPTPATH**
    - The folder path of current build.sh

## Definitions
```
IMAGE_TAG="lkg"
```
- default image tag
- User can use -t|--tag [name] to assign tag
- example
  - ./build.sh build_abl -t lkg

```
IMAGE_NAME="nhlos-hi2020"
```
- default 

```
RUNUSERID="--user $(id -u ${USER}):$(id -g ${USER}) "
```
- Assign variables for IMAGE_TAG, IMAGE_NAME ...
- ${USER}
   ```
   tony@tony-ST50:/android/zeta/c1/11/abl$ echo ${USER}
   tony
   ```
- id: print real and effective user and group ID
   ```
   tony@tony-ST50:/android/zeta/c1/11/abl$ id -u ${USER}
   1000
   tony@tony-ST50:/android/zeta/c1/11/abl$ id -g ${USER}
   1000
   tony@tony-ST50:/android/zeta/c1/11/abl$ echo $(id -u ${USER}):$(id -g ${USER})
   1000:1000
   ```
MAXCPU=""
BAREDOCKER=""
SKIPUPDATEDOCKER=""
FETCH=""
VERSION=""
DOCKERINTERACTIVE="-i"
TARGET="lahaina"

## Run docker - interactive or build
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
- if ./build.sh with -env, mount docker image with bash command.
  - A. ./build.sh build_abl -env
  - B. make TARGET=lahaina build_abl
- if no -env, run build directly

# The source code of build.sh

```
#!/bin/bash
SCRIPTPATH=`cd "$( dirname "${BASH_SOURCE[0]}" )" >/dev/null 2>&1 && pwd`
retval=0

IMAGE_TAG="lkg"
IMAGE_NAME="nhlos-hi2020"
RUNUSERID="--user $(id -u ${USER}):$(id -g ${USER}) "
MAXCPU=""
BAREDOCKER=""
SKIPUPDATEDOCKER=""
FETCH=""
VERSION=""
DOCKERINTERACTIVE="-i"
TARGET="lahaina"

POSITIONAL=()
while [[ $# -gt 0 ]]
do
key="$1"
    case $key in
        -t|--tag)
        IMAGE_TAG="$2"
        shift # past argument
        shift # past value
        ;;
        -n|--name)
        IMAGE_NAME="$2"
        shift # past argument
        shift # past value
        ;;
        -r|--root)
        RUNUSERID="--privileged"
        shift # past argument
        ;;    
        -j|--maxcpu)
        MAXCPU="-j $2"
        shift # past argument
        shift # past value
        ;;
        -env)
        BAREDOCKER="y"
        shift # past argument
        ;;
        -nopull)
        SKIPUPDATEDOCKER="y"
        shift # past argument
        ;;
        -fetch)
        FETCH="y"
        shift # past argument
        ;;
        -v|--version)
        VERSION="$2"
        shift # past argument
        shift # past value
        ;;
        -noninteractive)
        DOCKERINTERACTIVE=""
        shift
        ;; # past argument
        *)    # unknown option
        POSITIONAL+=("$1") # save it in an array for later
        shift # past argument
        ;;
    esac
done
set -- "${POSITIONAL[@]}" # restore positional parameters

#Expected not to change variables
IMAGE_PATH="${IMAGE_NAME}:${IMAGE_TAG}"
IMAGE_REPO="EOSBuildACR.azurecr.io"
PKG_IMAGE_PATH="e-azcli:lkg"
IMAGE_USER="2e2afb2b-2524-4868-b3c2-cf20b94d0bcb"
IMAGE_PWD="0486e6b6-035f-497f-9a51-20798b1e7614"
build_command="make TARGET=${TARGET} $MAXCPU $1"

echo -------------------------------------
echo NHLOS build.sh
echo -------------------------------------
echo IMAGE_TAG     = ${IMAGE_TAG}
echo IMAGE_NAME    = ${IMAGE_NAME}
echo RUNUSERID     = $RUNUSERID
echo MAXCPU        = ${MAXCPU}
echo BAREDOCKER    = ${BAREDOCKER}
echo IMAGE_PATH    = ${IMAGE_PATH}
echo IMAGE_REPO    = ${IMAGE_REPO}
echo PKG_IMAGE_PATH= ${PKG_IMAGE_PATH}
echo build_command = $build_command

if [ -z "$AZBUILDVER" ]; then
  export AZBUILDVER="0.0.0"
  echo "AZBUILDVER not defined, set to 0.0.0"
fi

if [ ! -z "$VERSION" ]; then
  echo "Override AZBUILDVER to $VERSION"
  export AZBUILDVER=$VERSION
fi
echo AZBUILDVER = $AZBUILDVER

if [ -z "$SKIPUPDATEDOCKER" ]; then
  echo "> Docker container repo login"
  docker login $IMAGE_REPO -u $IMAGE_USER -p $IMAGE_PWD
  retval=$?
  if [ $retval -ne 0 ]; then
      echo "docker login failed $retval"
      return $retval &>/dev/null || exit $retval
  fi
  echo "> Pull latest docker image for build"
  docker pull "$IMAGE_REPO/$IMAGE_PATH"
  retval=$?
  if [ $retval -ne 0 ]; then
      echo "docker pull failed $retval"
      return $retval &>/dev/null || exit $retval
  fi
  echo "> Pull latest docker image for pkg download"
  docker pull "$IMAGE_REPO/$PKG_IMAGE_PATH"
  retval=$?
  if [ $retval -ne 0 ]; then
      echo "docker pull failed $retval"
      return $retval &>/dev/null || exit $retval
  fi
else
  echo "> Skipping docker image pull"
fi

if [ ! -z "$FETCH" ]; then
  echo "> Fetching packages"
  if [ -z "$AZURE_DEVOPS_EXT_PAT" ]; then
    echo " - WARNING: AZURE_DEVOPS_EXT_PAT not set, please get a PAT token and set"
    exit 2
  fi
  docker run $DOCKERINTERACTIVE -t --mount type=bind,source=$SCRIPTPATH,target=/s -w=/s $RUNUSERID -e AZURE_DEVOPS_EXT_PAT "$IMAGE_REPO/$PKG_IMAGE_PATH" -c "make getpkg_nhlos"
  retval=$?
  if [ $retval -ne 0 ]; then
      echo "patckage fetch failed $retval"
      return $retval &>/dev/null || exit $retval
  fi
fi

echo "> Check Build Command"
if [ -z "$1" ]; then
    build_command="make $MAXCPU build_common_nonhlos_debug; bash scripts/copy-artifacts.sh"
    echo "No command specified - using default: $build_command"
fi

echo "> Building nhlos via docker"
echo "   - build_command: $build_command"
if [ -z "$BAREDOCKER" ]; then
  docker run $DOCKERINTERACTIVE -t --mount type=bind,source=$SCRIPTPATH,target=/s -w=/s $RUNUSERID -e AZBUILDVER -e AZBUILDVERINT "$IMAGE_REPO/$IMAGE_PATH" -c "$build_command"
else
  echo "   - Launching Docker Build environment only"
  docker run -it --mount type=bind,source=$SCRIPTPATH,target=/s -w=/s $RUNUSERID -e AZBUILDVER -e AZBUILDVERINT "$IMAGE_REPO/$IMAGE_PATH" -c "/bin/bash"
fi

```