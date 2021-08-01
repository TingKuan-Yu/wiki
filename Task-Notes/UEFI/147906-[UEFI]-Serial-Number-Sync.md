# keep soc serial number
- refer to 80-NM248-6 Rev. K
- refer to sectools debugpolicy.xml
- need soc serial number for fused debug to debug
- add an soc serial number could be useful if system can boot to fastboot but can't boot to os to get soc serial number.


# the concept of multi download edl flash script
  - programming one device a time
  - copy the specific partition 3 table with specific sfpd to images
  - pseudo code
```
#!/bin/bash
			
declare -A ufsserial_sfpd_array
ufsserial_sfpd_array["ufs_sn_1"]="spf_sn_1_rawprogram3.xml"
ufsserial_sfpd_array["ufs_sn_2"]="spf_sn_2_rawprogram3.xml"
ufsserial_sfpd_array["ufs_sn_3"]="spf_sn_3_rawprogram3.xml"


array=($(ls -1 /dev/ttyS*))
array2=($(ls -1 /dev/ttyUSB*))


for element in "${ufsserial_sfpd_array[@]}"
do
#echo "${element}: copy ${ufsserial_sfpd_array[${element}]}"
echo "${element}"
done

for element in "${array[@]}"
do
echo "get ufs serial"
echo "copy rawprogram3.xml"
echo "flash edl ${element}"
#$(which pwsh) -NoLogo -NoProfile -ExecutionPolicy Bypass -Command "${MY_PATH}/edl.ps1 edl_flash_bl ${element}"
done

for element in "${array2[@]}"
do
echo "get ufs serial"
echo "copy rawprogram3.xml"
echo "flash edl ${element}"
#$(which pwsh) -NoLogo -NoProfile -ExecutionPolicy Bypass -Command "${MY_PATH}/edl.ps1 edl_flash_bl ${element}"
done

```

# replace sfpd.img
```
root@UbuntM-VB:/media/sf_VBShare/images/2021.426.2-dev-combo# export SFSERIAL=sf123445678
root@UbuntM-VB:/media/sf_VBShare/images/2021.426.2-dev-combo# cp flashmap.developer.provision.json flashmap.${SFSERIAL}.provision.json
root@UbuntM-VB:/media/sf_VBShare/images/2021.426.2-dev-combo# cat flashmap.${SFSERIAL}.provision.json | grep sfpd.img
            "args": ["sfpd.img"]
root@UbuntM-VB:/media/sf_VBShare/images/2021.426.2-dev-combo# cat flashmap.${SFSERIAL}.provision.json | sed -e "s/sfpd.img/sfpd-$SFSERIAL.img/g" | grep sfpd
            "partitions": ["sfpd"],
            "args": ["sfpd-sf123445678.img"]

root@UbuntM-VB:/media/sf_VBShare/images/2021.426.2-dev-combo# sed -i "s/sfpd.img/sfpd-$SFSERIAL.img/g" flashmap.${SFSERIAL}.provision.json
root@UbuntM-VB:/media/sf_VBShare/images/2021.426.2-dev-combo# cat flashmap.${SFSERIAL}.provision.json | grep sfpd
            "partitions": ["sfpd"],
            "args": ["sfpd-sf123445678.img"]


```

