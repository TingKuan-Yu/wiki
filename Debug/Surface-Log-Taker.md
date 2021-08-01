
# Source Code Link
- https://dev.azure.com/E-OS/device/_git/bsp-tools?path=%2FSurfaceLogTaker

# Artificate
- https://dev.azure.com/E-OS/device/_packaging?_a=feed&feed=SurfaceLogTaker

# How to create Artifacts
## 1. To ADO artifacts
## 2. Press Create Feed to add SurfaceLogTaker
## 3. upload artificats
```
tingkuanyu@TonyYuLinux1:/E/debug_tools/device_bsp_tool/bsp-tools$ mv SurfaceLogTaker.tar.gz package/
tingkuanyu@TonyYuLinux1:/E/debug_tools/device_bsp_tool/bsp-tools$ cd package/
tingkuanyu@TonyYuLinux1:/E/debug_tools/device_bsp_tool/bsp-tools/package$ az artifacts universal publish --organization https://dev.azure.com/E-OS/ --project="device"  --scope project --feed SurfaceLogTaker --name surface-log-taker --version 0.0.2 --description "SurfaceLogTaker tools" --path .
{\ Uploading: 4596/4596 bytes: 100.00% ..
  "Description": "SurfaceLogTaker tools",
  "ManifestId": "3C60BA1811739337D7967564C6512AEB3B13D19EA5D8C934858C589AF539F44D01",
  "SuperRootId": "1944CC742B57CF5F88E8371480D199356247D58B5C478AE7C48C07F773C2198E02",
  "Version": "0.0.2"
}

```

# download artifacts
- https://dev.azure.com/E-OS/device/_packaging?_a=package&feed=SurfaceLogTaker&package=surface-log-taker&protocolType=UPack&version=0.0.2
```
az artifacts universal download --organization "https://dev.azure.com/E-OS/" --project "ce81bee4-8e73-47a6-9208-5f2cee8eb4d7" --scope project --feed "SurfaceLogTaker" --name "surface-log-taker" --version "0.0.2" --path .
```