
# A. Piplines -> All -> BSP code-integration
- https://dev.azure.com/E-OS/device/_build?definitionScope=%5CBSP-code-integration
  - a. create-branch
  - b. create-repo-list
  - c. create-patch
  - d. apply-patch
  - e. run-pipeline-build

# B. Piplines -> All -> c1 -> 11.0 -> manifest -> build
- https://dev.azure.com/E-OS/device/_build?definitionScope=%5Cc1%5C11.0%5Cmanifest%5Cbuild
  - a. hlos
    - (1). c1-11-kernel-build
    - (2). c1-11-vendor-build
  - b. image
    - (1). c1-11-merge-build
    - (2). c1-11-qssi-merge-build
  - c. nhlos
    - (1). c1-11-abl-build
    - (2). c1-11-adsp-build
    - (3). c1-11-aop-build
    - (4). c1-11-apdp-build
    - (5). c1-11-boot-build
    - (6). ...

# C. Artifacts -> code-integration
- a. c1-apply (Result for apply-patch)
- b. c1-branch
- c. c1-commit-diff
- d. c1-manifest
- e. c1-patch (Result for create-patch)
- f. skip-mte-manifest

# D. Artifacts -> c1-int-11-images (Result for run-piple-build)
- a. c1-11-developer-edl
- b. c1-11-developer-combo
- c. ...
- d. Patch Check List: https://microsoft-my.sharepoint.com/:x:/p/fangruwu/EVJYq4P479NPo_Wy68-yi6sBLPniYhFEJ8J4TZwSBhQhXA 