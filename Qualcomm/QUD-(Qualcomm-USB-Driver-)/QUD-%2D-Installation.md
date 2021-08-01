
# ubuntu 20 fail.
# ubunt 18 -> 20 success


# 1. install mono
- Ubuntu 20.04 (amd64, armhf, arm64, ppc64el)
```
sudo apt install gnupg ca-certificates
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 3FA7E0328081BFF6A14DA29AA6A19B38D3D831EF
echo "deb https://download.mono-project.com/repo/ubuntu stable-focal main" | sudo tee /etc/apt/sources.list.d/mono-official-stable.list
sudo apt update
sudo apt install mono-devel
```

# 2. Install QualcommPackageManager.LNX.2.0
- download keyring0 packages
https://packages.ubuntu.com/bionic/amd64/libgnome-keyring0/download
https://packages.ubuntu.com/bionic/amd64/libgnome-keyring-common/download
https://packages.ubuntu.com/bionic/amd64/multiarch-support/download
- install packages
```
sudo apt install ./*keyring*.deb ./multiarch*.deb
```
- download QualcommPackageManager.LNX.2.0 from qualcomm web
- install QualcommPackageManager.LNX.2.0
```
sudo dpkg -i QualcommPackageManager.2.0.27.1.Linux-x86.deb
```

# 3. install packages and drivers
- Login QPM
  - qpm-cli --login <user-name>
```
tingkuanyu@TKubunt20:/E/QCT/Tools/Ubuntu-tools$ qpm-cli --login tingkuanyu@microsoft.com
Password: ********
[Info] : Login is successful
[Info] : Fetching product catalog ....
[Info] : Product catalog refreshed successfully
```
- Check if a user have access to the QUD, QUTS and PCAT tools.
  - qpm-cli --product-list
```
tingkuanyu@TKubunt20:/E/QCT/Tools/Ubuntu-tools$ qpm-cli --product-list
---- List of products ----
audio1.x
compute1.x
eai
halide2.3
hexagon8.4
hexagon8.5
hexagonsdk4
hexagonsdk4.x
pcat
qcap
qcat
qdte
qpm
qualcomm_snapdragon_llvm_arm_toolchain_oem
qud
quts
qxdm
qxdm5
```
- Activate QUD, QUTS and PCAT licenses

qpm-cli --license-activate qud
```
tingkuanyu@TKubunt20:/E/QCT/Tools/Ubuntu-tools$ qpm-cli --license-activate qud
[Info] : Activating license : qud
[Info] : License was already activated, ActivationId=242b1ab8-b242-11eb-981b-02c1fc0264f7
```
qpm-cli --license-activate quts
```
tingkuanyu@TKubunt20:/E/QCT/Tools/Ubuntu-tools$ qpm-cli --license-activate quts
[Info] : Activating license : quts
[Info] : License was already activated, ActivationId=242b1ab8-b242-11eb-981b-02c1fc0264f7
```
qpm-cli --license-activate pcat
```
tingkuanyu@TKubunt20:/E/QCT/Tools/Ubuntu-tools$ qpm-cli --license-activate pcat
[Info] : Activating license : pcat
[Info] : License was already activated, ActivationId=21cc88ff-b242-11eb-981b-02c1fc0264f7
```
- Install QUD, QUTS and PCAT
  - qpm-cli --install qud
  - qpm-cli --install quts
  - qpm-cli --install pcat

- Install Crash Analysis Tool
  - sudo qpm-cli --install qcap
  - opened http://security.ubuntu.com/ubuntu/pool/main/o/openssl1.0/ in my browser and download last version of libssl1.0.0 for my system (for me it was libssl1.0.0_1.0.2n-1ubuntu5.6_amd64.deb) Then I just install it:
```
ingkuanyu@TKubunt20:/E/QCT/Tools/Ubuntu-tools$ sudo dpkg -i libssl1.0.0_1.0.2n-1ubuntu5.6_amd64.deb
Selecting previously unselected package libssl1.0.0:amd64.
(Reading database ... 295814 files and directories currently installed.)
Preparing to unpack libssl1.0.0_1.0.2n-1ubuntu5.6_amd64.deb ...
Unpacking libssl1.0.0:amd64 (1.0.2n-1ubuntu5.6) ...
Setting up libssl1.0.0:amd64 (1.0.2n-1ubuntu5.6) ...
Processing triggers for libc-bin (2.31-0ubuntu9.2) ...
```
- tcsh

# Ubuntu20 fail

# reference
- KBA-201209020550
- 