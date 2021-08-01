# Docker list
##  docker image ls [OPTIONS] [REPOSITORY[:TAG]]
```
tony@tony-ST50:/android/msprj/c1/11/abl$ docker image ls
REPOSITORY                            TAG       IMAGE ID       CREATED         SIZE
ubuntu                                latest    7e0aa2d69a15   2 weeks ago     72.7MB
android-build-16.04                   latest    3ee79dff87e2   8 weeks ago     772MB
ubuntu                                16.04     8185511cd5ad   3 months ago    132MB
EOSBuildACR.azurecr.io/nhlos-hi2020   lkg       e6df58953b9c   4 months ago    10.4GB
EOSBuildACR.azurecr.io/e-azcli        lkg       5b8aecc1e55c   6 months ago    1.64GB
EOSBuildACR.azurecr.io/hlos-eos-11    lkg       b210ca293589   7 months ago    1.25GB
```
- EOSBuildACR.azurecr.io/nhlos-hi2020
- EOSBuildACR.azurecr.io/nhlos-hi2020
- EOSBuildACR.azurecr.io/hlos-eos-11

## docker pull [OPTIONS] NAME[:TAG|@DIGEST]
- example usage: $ docker pull myregistry.local:5000/testing/test-image\
- EOSBuildACR.azurecr.io: MS repository
```
tony@tony-ST50:/android/msprj/c1/11/abl$ docker pull EOSBuildACR.azurecr.io/nhlos-hi2020
Using default tag: latest
latest: Pulling from nhlos-hi2020
Digest: sha256:1e26bcf440f54c1ede51d4b263e53215c9a1d7f40d8a3f51419508816c852b10
Status: Downloaded newer image for EOSBuildACR.azurecr.io/nhlos-hi2020:latest
EOSBuildACR.azurecr.io/nhlos-hi2020:latest
```