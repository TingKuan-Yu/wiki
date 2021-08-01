# How to Backup and Restor QCN
https://dev.azure.com/DSQO-Taipei/Knowledge%20Share/_wiki/wikis/Knowledge-Share.wiki/8/How-to-backup-restore-QCN-Zeta

# QFIL Method
## QCN BACKUP
- .\QFIL.exe -COM=5 -Mode=3 -QCNPATH="c:\VBShare\tmp\test.qcn" -BACKUPQCN -WORKPATH="c:\VBShare\tmp" -LOGFILEPATH="c:\VBShare\tmp"
```
PS C:\Program Files (x86)\Qualcomm\QPST\bin> .\QFIL.exe -COM=5 -Mode=3 -QCNPATH="c:\VBShare\tmp\test.qcn" -BACKUPQCN -WORKPATH="c:\VBShare\tmp" -LOGFILEPATH="c:\VBShare\tmp"
Loading parameters may takes few minutes, please wait...
2021-05-11 15:40:06.236    ***** Working Folder:C:\Users\tingkuanyu\AppData\Roaming\Qualcomm\QFIL\BHI
2021-05-11 15:40:06.236    WORKPATH:c:\VBShare\tmp
2021-05-11 15:40:06.236    MODE:3
2021-05-11 15:40:06.236    LOGFILEPATH:c:\VBShare\tmp
2021-05-11 15:40:06.236    Validating Application Configuration
2021-05-11 15:40:06.252    Load APP Configuration
2021-05-11 15:40:06.267    COM:5
2021-05-11 15:40:06.267    PBLDOWNLOADPROTOCOL:0
2021-05-11 15:40:06.267    PROGRAMMER:True
:
:
2021-05-11 15:41:50.220    Subscription ID:0 EFS File:/nv/item_files/modem/sms/cs_domain_fallback, Function:BackupNV_WriteNVsToQCN, Event:13  70%
2021-05-11 15:41:50.733    Done downloading the qcn file: c:\VBShare\tmp\test.qcn
2021-05-11 15:41:50.741
2021-05-11 15:41:50.754    Backup QCN Succeed
2021-05-11 15:41:50.755    Finish Backup QCN

```
  - Parametes
    - BACKUPQCN
    - RESTOREQCN
    - LOGFILEPATH
    - WORKPATH
    - COM
    - Mode
       0 – Normal mode
       1 – Engineer mode
       2 – Not supported
       3 – Silent mode
    -QCNPATH
       - Qfil.exe -QCNPATH=“C:\VBShare\tmp\test.qcn” QCN path for manual backup/restore

## QCN RESTORE
```
PS C:\Program Files (x86)\Qualcomm\QPST\bin> .\QFIL.exe -COM=5 -Mode=3 -QCNPATH="c:\VBShare\tmp\test.qcn" -RESTOREQCN -WORKPATH="c:\VBShare\tmp" -LOGFILEPATH="c:\VBShare\tmp"
Loading parameters may takes few minutes, please wait...
2021-05-11 15:46:33.942    ***** Working Folder:C:\Users\tingkuanyu\AppData\Roaming\Qualcomm\QFIL\BHI
2021-05-11 15:46:33.957    WORKPATH:c:\VBShare\tmp
2021-05-11 15:46:33.957    MODE:3
2021-05-11 15:46:33.957    LOGFILEPATH:c:\VBShare\tmp
2021-05-11 15:46:33.957    Validating Application Configuration
2021-05-11 15:46:33.957    Load APP Configuration
2021-05-11 15:46:33.973    COM:5
2021-05-11 15:46:33.973    PBLDOWNLOADPROTOCOL:0
2021-05-11 15:46:33.973    PROGRAMMER:True
:
:
2021-05-11 15:46:46.413    Subscription ID:0 EFS File:/nv/item_files/wcdma/wcdma_srp_cqi_boosting_control, Function:NV_Tool_WriteNVsToMobile, Event:2  47%
2021-05-11 15:46:46.413    Done uploading the QCN file: c:\VBShare\tmp\test.qcn, Sync EFS
2021-05-11 15:46:46.932    Done EFS Sync
2021-05-11 15:46:46.950
2021-05-11 15:46:46.950    Restore Succeed
2021-05-11 15:46:46.951    Finish Restore QCN
```

