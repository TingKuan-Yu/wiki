# Get abl manifest
- https://dev.azure.com/E-OS/device/_packaging?_a=package&feed=c1-11-main-manifest%40Local&package=abl-manifest&protocolType=UPack&version=2021.519.2&view=overview
- example
``` 
az artifacts universal download --organization "https://dev.azure.com/E-OS/" --feed "c1-11-main-manifest" --name "abl-manifest" --version "2021.519.2" --path .
```

# generate a bare git repository
```
mkdir abl.git
git init --bare
```

# git clone the repo
```
git clone abl.git abl.clone
```

# add abl-manifest.xml and push
```
cp abl-manifest.xml abl.clone
cd abl.clone
git add abl-manifest.xml
git commit -m "abl-manifest 2021.519.2"
git push
git tag 2021.519.2
git push --tag
```

# repo init and sync abl
```
mkdir abl_dev
cd abl_dev
repo init -u ../abl.git -m abl-manifest.xml
cd .repo/manifests
git reset --hard 2021.519.2
cd ../..
repo sync -c
```