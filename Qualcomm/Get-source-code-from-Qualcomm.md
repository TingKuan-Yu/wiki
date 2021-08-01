# Qualcomm ChipCode
- Android 11 for Zeta: snapdragon-premium-high-2020-spf-1-0_amss_standard_oem
  - https://chipcode.qti.qualcomm.com/microsoft-corporation/snapdragon-premium-high-2020-spf-1-0_amss_standard_oem/tree/r1.0.c8_00005.9

# clone issue
 - Need to set "git config --global http.followRedirects true" for git clone
 - Incrementing buffer size might help, try: git config --global http.postBuffer 524288000
 - https://stackoverflow.com/questions/65174787/gpg-cant-check-signature-no-public-key-upon-initializing-a-repo-from-code-a
   - **_Drop the_** --repo-url=git://codeaurora.org/tools/repo.git --repo-branch=caf-stable from your repo init command.


# Get Release Note
- example: 
https://createpoint.qti.qualcomm.com/planner/#pkSelectedSummary/searchArgs/rows||5||sortField||releaseDate||sortOrder||desc||isSpf||true||releaseName||Snapdragon_Premium_High_2020.SPF.1.0||buildTag||r1.0.r1_00036.0||branch||master||product||LAHAINA.LA.1.1||customerName||Microsoft%20Corporation||projectName||Zeta||customer||225775||fq_softwareProduct||LAHAINA.LA.1.1||fq_customerName||Microsoft%20Corporation
![Screenshot at 2021-05-19 14-06-04.png](/.attachments/Screenshot%20at%202021-05-19%2014-06-04-387971ba-c360-421e-a7e9-524d31fe00e6.png)