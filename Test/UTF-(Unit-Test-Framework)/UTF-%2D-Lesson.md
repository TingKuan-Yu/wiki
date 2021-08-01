# 1. Multi-devices issues
- @bert Amy Tang 在getprop 時加了 ${UTF_HOST_DEVICE_SERIAL_NUMBER} https://dev.azure.com/E-OS/tools/_git/utf-subsystems/pullrequest/24834
- 另現在local uft test. Makefile 內自行加device= 如python3 utftests.py -y ../../yamltests/$(path) -o ../../testresults.trx --device=SFB1BC8666FA3F 可測單一device, 如此便可check device有沒有真的認到.
- console 可看到如下有帶device= 的log Got 202 response from: http://localhost:8080/api/Core/RunCTSTest?module=CtsContentSuggestionsTestCases&SkipSetup=True&device=SFB1BC8666FA3 
- 找不到實際帶 ${​​​​​​UTF_HOST_DEVICE_SERIAL_NUMBER}​​​​​​的地方. 懷疑utf內有binary code 來實作. 
- use log-info to show log in index.html