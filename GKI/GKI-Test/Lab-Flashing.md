```
[4:58 PM] Ziv Liu
1.Flash c1-11-selfhost-comboaz artifacts universal download --organization "https://dev.azure.com/E-OS/" --feed "c1-11-main-images" --name "c1-11-selfhost-combo" --version "2021.617.7" --path .chmod 775 *.sh./flash_test_perf.sh

2.Flash GSI imagesadb rootadb disable-verityadb reboot fastbootaz artifacts universal download --organization "https://dev.azure.com/E-OS/" --feed "xts-lab-tpe" --name "android-gsi" --version "2021.7.0" --path .fastboot --disable-verification flash vbmeta vbmeta.imgfastboot flash system system.imgfastboot flash boot boot-5.4.img

3.Flash GKI imagesaz pipelines runs artifact download --org "https://dev.azure.com/E-OS/" --project "device" --run-id "710258" --artifact-name "vendor" --path .cd out/dist/ && unzip oemc1-target_files-0.0.0.zip "IMAGES/*" && cd IMAGES/fastboot flash vendor vendor.imgfastboot flash odm odm.imgfastboot reboot bootloaderClick to download multi-pr-combo.zip from https://dev.azure.com/E-OS/ce81bee4-8e73-47a6-9208-5f2cee8eb4d7/_apis/build/builds/710258/artifacts?artifactName=multi-pr-combo&api-version=6.0&%24format=zipunzip multi-pr-combo.zip && cd multi-pr-combo/bin/fastboot flash vendor_boot vendor_boot-debug.imgfastboot -wfastboot reboot





```