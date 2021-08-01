# Establish-build-environment
https://dev.azure.com/E-OS/device/_wiki/wikis/Wiki/25645/Establish-build-environment


# Linux VPN Setup
https://linux-scripts.visualstudio.com/MSVPN-linux

# Ubuntu Docker Installation
https://docs.docker.com/engine/install/ubuntu/

# Python Switch
```
tony@tony-ST50:~/bin$ sudo update-alternatives --install /usr/bin/python python /usr/bin/python2 1
tony@tony-ST50:~/bin$ sudo update-alternatives --install /usr/bin/python python /usr/bin/python3 2
tony@tony-ST50:~/bin$ sudo update-alternatives --config python
```

# Android Repo issue
 
```
curl https://storage.googleapis.com/git-repo-downloads/repo > ~/bin/repo
gpg --keyserver hkps://keyserver.ubuntu.com --recv-key 8BB9AD793E8E6153AF0F9A4416530D5E920F5C65
curl https://storage.googleapis.com/git-repo-downloads/repo.asc | gpg --verify - ~/bin/repo
```

2. rm ~/.repoconfig

# shell language
- export LC_ALL=C
  - unset LC_ALL


# build error fix:
1) missing libncurses5.so
sudo add-apt-repository universe
sudo apt-get install libncurses5 libncurses5:i386 

