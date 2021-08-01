[[_TOC_]]


# initcall message in dmesg
- BOARD_KERNEL_CMDLINE += initcal_debug
- sort dmesg:
```
  cat dmesg.txt | grep "initcall" | sed "s/\(.*\)after\(.*\)/\2 \1/g" | sort -n
```

# sort android property
```
adb shell getprop > getprop.txt 
cat getprop.txt | grep boottime > bootime.txt 
sed -e 's/\[/ /g; s/\]/ /g; s/\:/ /g' bootime.txt | sort -k2 -n > bootime-sorted.txt
```