# git push test
```
tony@tony-ST50:/android/mstkgit$ git clone git@ssh.dev.azure.com:v3/tingkuanyu/TingKuanYuPrivate1/TingKuanYuPrivate1 -b testbranch1
正複製到 'TingKuanYuPrivate1'...
remote: Azure Repos
remote: Found 10 objects to send. (31 ms)
接收物件中: 100% (10/10), 5.50 KiB | 5.50 MiB/s, 完成.
處理 delta 中: 100% (1/1), 完成.

tony@tony-ST50:/android/mstkgit/TingKuanYuPrivate1$ ls
favorites_2021_4_11.html  gittest.txt
tony@tony-ST50:/android/mstkgit/TingKuanYuPrivate1$ git branch
* testbranch1
tony@tony-ST50:/android/mstkgit/TingKuanYuPrivate1$ ls
favorites_2021_4_11.html  gittest.txt
tony@tony-ST50:/android/mstkgit/TingKuanYuPrivate1$ cat gittest.txt 
V1
review_test
tony@tony-ST50:/android/mstkgit/TingKuanYuPrivate1$ echo testv1-1 >> gittest.txt 
tony@tony-ST50:/android/mstkgit/TingKuanYuPrivate1$ git status
位於分支 testbranch1
您的分支與上游分支 'origin/testbranch1' 一致。

尚未暫存以備提交的變更：
  （使用 "git add <檔案>..." 更新要提交的內容）
  （使用 "git restore <檔案>..." 捨棄工作區的改動）
	修改：     gittest.txt

修改尚未加入提交（使用 "git add" 和/或 "git commit -a"）
tony@tony-ST50:/android/mstkgit/TingKuanYuPrivate1$ git add .
tony@tony-ST50:/android/mstkgit/TingKuanYuPrivate1$ git commit -m "testv1-1"
[testbranch1 a4c65c2] testv1-1
 1 file changed, 1 insertion(+)
tony@tony-ST50:/android/mstkgit/TingKuanYuPrivate1$ git remote
origin
tony@tony-ST50:/android/mstkgit/TingKuanYuPrivate1$ git branch
* testbranch1
tony@tony-ST50:/android/mstkgit/TingKuanYuPrivate1$ git push origin testbranch1
枚舉物件: 5, 完成.
物件計數中: 100% (5/5), 完成.
使用 12 個執行緒進行壓縮
壓縮物件中: 100% (2/2), 完成.
寫入物件中: 100% (3/3), 278 位元組 | 278.00 KiB/s, 完成.
總共 3 （差異 1），復用 0 （差異 0）
remote: Analyzing objects... (3/3) (17 ms)
remote: Storing packfile... done (194 ms)
remote: Storing index... done (30 ms)
To ssh.dev.azure.com:v3/tingkuanyu/TingKuanYuPrivate1/TingKuanYuPrivate1
   92ed3d5..a4c65c2  testbranch1 -> testbranch1
```