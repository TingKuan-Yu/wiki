

- git clone git@ssh.dev.azure.com:v3/E-OS/device/manifest -b sm8350/11/main
  - older version than hi2020/11/main

- git clone git@ssh.dev.azure.com:v3/E-OS/device/manifest -b hi2020/11/main
  - toplogy is similar as sm8350/11/main
  - content is newer than sm8350/11/main

- git clone git@ssh.dev.azure.com:v3/E-OS/device/manifest -b c1/11/main
  - main branch for daily use.

- git clone git@ssh.dev.azure.com:v3/E-OS/device/manifest -b c1/int/11/c8_00005.9
  - integration branch for merge newer Qualcomm code base
  - This branch is a new branch from c1/11/main, so the topology is the same as the c1/11/main.
  - Need to change below fild for integration 
    - c1/11/main -> c1/int/11/c8_00005.9
    - always: true -> always: false
      - The int branch needn't peridicly build.
    -  prRepoOrigin: device --> prRepoOrigin: device-qcom
      - @TODO: need more check