# Pull Request 27173: Add Vendor_User_GKI_VendorBoot
- https://dev.azure.com/E-OS/device/_git/manifest/pullrequest/27173?_a=commits
```

114 Minus		          cmd: 'eos_build/scripts/build.sh -skipdocker -l oemc1-gki -v $(Build.BuildNumber) -sku default vendorbootimage'
114 Plus		          cmd: 'eos_build/scripts/build.sh -skipdocker -l oemc1-gki -v $(Build.BuildNumber) -sku default vendorbootimage vendorbootdebugimage'
```