[[_TOC_]]

# git init --bare
```
tony@tony-ST50:~/gerrit_readme/git_local_test/test.git$ git init --bare
已初始化空的 Git 版本庫於 /home/tony/gerrit_readme/git_local_test/test.git/

tony@tony-ST50:~/gerrit_readme/git_local_test/test.git$ ls
branches  config  description  HEAD  hooks  info  objects  refs

tony@tony-ST50:~/gerrit_readme/git_local_test/test.git/refs$ tree
.
├── heads
└── tags

tony@tony-ST50:~/gerrit_readme/git_local_test$ git clone test.git test_clone
正複製到 'test_clone'...
warning: 您似乎複製了一個空版本庫。
完成。

tony@tony-ST50:~/gerrit_readme/git_local_test$ cd test_clone/
tony@tony-ST50:~/gerrit_readme/git_local_test/test_clone$ ls
tony@tony-ST50:~/gerrit_readme/git_local_test/test_clone$ ls .
./    ../   .git/ 
tony@tony-ST50:~/gerrit_readme/git_local_test/test_clone$ ls .git/config 
.git/config
tony@tony-ST50:~/gerrit_readme/git_local_test/test_clone$ cat .git/config 
[core]
	repositoryformatversion = 0
	filemode = true
	bare = false
	logallrefupdates = true
[remote "origin"]
	url = /home/tony/gerrit_readme/git_local_test/test.git
	fetch = +refs/heads/*:refs/remotes/origin/*
[branch "master"]
	remote = origin
	merge = refs/heads/master

tony@tony-ST50:~/gerrit_readme/git_local_test/test.git$ cat HEAD 
ref: refs/heads/master

tony@tony-ST50:~/gerrit_readme/git_local_test/test_clone$ cat .git/HEAD 
ref: refs/heads/master


tony@tony-ST50:~/gerrit_readme/git_local_test/test_clone$  echo "my name is tony" > tony_yu.txt
tony@tony-ST50:~/gerrit_readme/git_local_test/test_clone$ git add .
tony@tony-ST50:~/gerrit_readme/git_local_test/test_clone$ git commit -m "preliminary checkin"
[master (根提交) 936d475] preliminary checkin
 1 file changed, 1 insertion(+)
 create mode 100644 tony_yu.txt
tony@tony-ST50:~/gerrit_readme/git_local_test/test_clone$ ls
tony_yu.txt

tony@tony-ST50:~/gerrit_readme/git_local_test/test_clone$ git branch
* master

tony@tony-ST50:~/gerrit_readme/git_local_test/test_clone$ git log
commit 936d4754a2d0a1b64e3bb9778e280c58e878f579 (HEAD -> master)
Author: tony1_yu <580en070@ntut.org.tw>
Date:   Fri Apr 2 19:25:46 2021 +0800

    preliminary checkin

tony@tony-ST50:~/gerrit_readme/git_local_test/test_clone$ git push origin master
枚舉物件: 3, 完成.
物件計數中: 100% (3/3), 完成.
寫入物件中: 100% (3/3), 235 位元組 | 235.00 KiB/s, 完成.
總共 3 （差異 0），復用 0 （差異 0）
To /home/tony/gerrit_readme/git_local_test/test.git
 * [new branch]      master -> master

tony@tony-ST50:~/gerrit_readme/git_local_test/test_clone$ git branch test1
tony@tony-ST50:~/gerrit_readme/git_local_test/test_clone$ git branch
* master
  test1
tony@tony-ST50:~/gerrit_readme/git_local_test/test_clone$ git checkout test1 
切換到分支 'test1'
tony@tony-ST50:~/gerrit_readme/git_local_test/test_clone$ git branch
  master
* test1

tony@tony-ST50:~/gerrit_readme/git_local_test/test_clone$ tree .git/
.git/
├── branches
├── COMMIT_EDITMSG
├── config
├── description
├── HEAD
├── hooks
│   ├── applypatch-msg.sample
│   ├── commit-msg.sample
│   ├── fsmonitor-watchman.sample
│   ├── post-update.sample
│   ├── pre-applypatch.sample
│   ├── pre-commit.sample
│   ├── pre-merge-commit.sample
│   ├── prepare-commit-msg.sample
│   ├── pre-push.sample
│   ├── pre-rebase.sample
│   ├── pre-receive.sample
│   └── update.sample
├── index
├── info
│   └── exclude
├── logs
│   ├── HEAD
│   └── refs
│       ├── heads
│       │   ├── master
│       │   └── test1
│       └── remotes
│           └── origin
│               └── master
├── objects
│   ├── 93
│   │   └── 6d4754a2d0a1b64e3bb9778e280c58e878f579
│   ├── 98
│   │   └── 54eb00d6d84f5e2854217ab82ad5d168453c3a
│   ├── a0
│   │   └── 8b6785b6a42ab6f4e5e78d7e3dd0910c2eba5d
│   ├── info
│   └── pack
└── refs
    ├── heads
    │   ├── master
    │   └── test1
    ├── remotes
    │   └── origin
    │       └── master
    └── tags

19 directories, 28 files

tony@tony-ST50:~/gerrit_readme/git_local_test/test_clone$ git checkout master
切換到分支 'master'
您的分支與上游分支 'origin/master' 一致。


tony@tony-ST50:~/gerrit_readme/git_local_test/test_clone$ git tag v1
tony@tony-ST50:~/gerrit_readme/git_local_test/test_clone$ git tag
v1

tony@tony-ST50:~/gerrit_readme/git_local_test/test_clone$  git tag -l 
v1
tony@tony-ST50:~/gerrit_readme/git_local_test/test_clone$ git show v1
commit 936d4754a2d0a1b64e3bb9778e280c58e878f579 (HEAD -> master, tag: v1, origin/master, test1)
Author: tony1_yu <580en070@ntut.org.tw>
Date:   Fri Apr 2 19:25:46 2021 +0800

    preliminary checkin

diff --git a/tony_yu.txt b/tony_yu.txt
new file mode 100644
index 0000000..9854eb0
--- /dev/null
+++ b/tony_yu.txt
@@ -0,0 +1 @@
+my name is tony
tony@tony-ST50:~/gerrit_readme/git_local_test/test_clone$ git add .
tony@tony-ST50:~/gerrit_readme/git_local_test/test_clone$ git commit -m "test"
[master c72d7b1] test
 1 file changed, 1 insertion(+)


tony@tony-ST50:~/gerrit_readme/git_local_test/test_clone$ git push origin v1
總共 0 （差異 0），復用 0 （差異 0）
To /home/tony/gerrit_readme/git_local_test/test.git
 * [new tag]         v1 -> v1
``` 
 
# test v2
```
tony@tony-ST50:~/gerrit_readme/git_local_test/test_clone$ echo test >> tony_yu.txt 
tony@tony-ST50:~/gerrit_readme/git_local_test/test_clone$ cat tony_yu.txt 
my name is tony
test

tony@tony-ST50:~/gerrit_readme/git_local_test/test_clone$ git tag v2
tony@tony-ST50:~/gerrit_readme/git_local_test/test_clone$ git tag -l
v1
v2

tony@tony-ST50:~/gerrit_readme/git_local_test/test_clone$ git push origin +refs/heads/* +refs/tags/*
枚舉物件: 5, 完成.
物件計數中: 100% (5/5), 完成.
寫入物件中: 100% (3/3), 258 位元組 | 258.00 KiB/s, 完成.
總共 3 （差異 0），復用 0 （差異 0）
To /home/tony/gerrit_readme/git_local_test/test.git
   936d475..c72d7b1  master -> master
 * [new branch]      test1 -> test1
 * [new tag]         v2 -> v2

tony@tony-ST50:~/gerrit_readme/git_local_test$ git clone test.git test_clone_v2
正複製到 'test_clone_v2'...
完成。
tony@tony-ST50:~/gerrit_readme/git_local_test$ cd test_clone_v2/
tony@tony-ST50:~/gerrit_readme/git_local_test/test_clone_v2$ git tag -l
v1
v2

tony@tony-ST50:~/gerrit_readme/git_local_test/test_clone_v2$ git log --oneline
c72d7b1 (HEAD -> master, tag: v2, origin/master, origin/HEAD) test
936d475 (tag: v1, origin/test1) preliminary checkin
```

# tag test v3
```
tony@tony-ST50:~/gerrit_readme/git_local_test/test_clone_v2$ git branch
* master

tony@tony-ST50:~/gerrit_readme/git_local_test/test_clone_v2$ git branch testv3

tony@tony-ST50:~/gerrit_readme/git_local_test/test_clone_v2$ git checkout testv3
切換到分支 'testv3'

tony@tony-ST50:~/gerrit_readme/git_local_test/test_clone_v2$ git branch
  master
* testv3

tony@tony-ST50:~/gerrit_readme/git_local_test/test_clone_v2$ echo testv3 >> tony_yu.txt 

tony@tony-ST50:~/gerrit_readme/git_local_test/test_clone_v2$ cat tony_yu.txt 
my name is tony
test
testv3

tony@tony-ST50:~/gerrit_readme/git_local_test/test_clone_v2$ git add .
tony@tony-ST50:~/gerrit_readme/git_local_test/test_clone_v2$ git commit -m "v3 checking"
[testv3 1fc516d] v3 checking
 1 file changed, 1 insertion(+)
tony@tony-ST50:~/gerrit_readme/git_local_test/test_clone_v2$ git branch
  master
* testv3
tony@tony-ST50:~/gerrit_readme/git_local_test/test_clone_v2$ git checkout master
切換到分支 'master'
您的分支與上游分支 'origin/master' 一致。

tony@tony-ST50:~/gerrit_readme/git_local_test/test_clone_v2$ git merge testv3
更新 c72d7b1..1fc516d
Fast-forward
 tony_yu.txt | 1 +
 1 file changed, 1 insertion(+)

tony@tony-ST50:~/gerrit_readme/git_local_test$ git clone test.git test_v3
正複製到 'test_v3'...
完成。

tony@tony-ST50:~/gerrit_readme/git_local_test/test_v3$ git log --oneline
1fc516d (HEAD -> master, tag: v3, origin/testv3, origin/master, origin/HEAD) v3 checking
c72d7b1 (tag: v2) test
936d475 (tag: v1, origin/test1) preliminary checkin
tony@tony-ST50:~/gerrit_readme/git_local_test/test_v3$ git tag
v1
v2
v3
```


# branch tonydev test
```
tony@tony-ST50:~/gerrit_readme/git_local_test/test_v3$ git branch
* master
tony@tony-ST50:~/gerrit_readme/git_local_test/test_v3$ git branch tonydev
tony@tony-ST50:~/gerrit_readme/git_local_test/test_v3$ git checkout tonydev
切換到分支 'tonydev'
tony@tony-ST50:~/gerrit_readme/git_local_test/test_v3$ git branch
  master
* tonydev
tony@tony-ST50:~/gerrit_readme/git_local_test/test_v3$ git push -u origin tonydev
總共 0 （差異 0），復用 0 （差異 0）
To /home/tony/gerrit_readme/git_local_test/test.git
 * [new branch]      tonydev -> tonydev
分支 'tonydev' 設定為追蹤來自 'origin' 的遠端分支 'tonydev'。


tony@tony-ST50:~/gerrit_readme/git_local_test$ history  | grep clone
 1422  git clone "https://gitee.com/wszqkzqk/deepin-wine-for-ubuntu.git"
 1581  git clone https://github.com/TingKuan-Yu/PythonT.git 
 2004  history | grep clone
 2010  git clone test.git test_v3
 2023  history  | grep clone
tony@tony-ST50:~/gerrit_readme/git_local_test$ git clone test.git -b tonydev test-b_tonydev
正複製到 'test-b_tonydev'...
完成。
tony@tony-ST50:~/gerrit_readme/git_local_test$ cd test-b_tonydev/
tony@tony-ST50:~/gerrit_readme/git_local_test/test-b_tonydev$ git branch
* tonydev
```

# branch tonydev test - tonydev_v1 tag
```
tony@tony-ST50:~/gerrit_readme/git_local_test/test-b_tonydev$ echo tonydev_v1_tag >> tony_yu.txt 
tony@tony-ST50:~/gerrit_readme/git_local_test/test-b_tonydev$ git add .
tony@tony-ST50:~/gerrit_readme/git_local_test/test-b_tonydev$ git commit -m "tonydev: v1_tag test"
[tonydev c8bb49c] tonydev: v1_tag test
 1 file changed, 1 insertion(+)
tony@tony-ST50:~/gerrit_readme/git_local_test/test-b_tonydev$ git tag tonydev_v1
tony@tony-ST50:~/gerrit_readme/git_local_test/test-b_tonydev$ git tag
tonydev_v1
v1
v2
v3
tony@tony-ST50:~/gerrit_readme/git_local_test/test-b_tonydev$ cat .git/config 
[core]
	repositoryformatversion = 0
	filemode = true
	bare = false
	logallrefupdates = true
[remote "origin"]
	url = /home/tony/gerrit_readme/git_local_test/test.git
	fetch = +refs/heads/*:refs/remotes/origin/*
[branch "tonydev"]
	remote = origin
	merge = refs/heads/tonydev
tony@tony-ST50:~/gerrit_readme/git_local_test/test-b_tonydev$ git push origin +refs/heads/* +refs/tags/*
枚舉物件: 5, 完成.
物件計數中: 100% (5/5), 完成.
寫入物件中: 100% (3/3), 286 位元組 | 286.00 KiB/s, 完成.
總共 3 （差異 0），復用 0 （差異 0）
To /home/tony/gerrit_readme/git_local_test/test.git
   1fc516d..c8bb49c  tonydev -> tonydev
 * [new tag]         tonydev_v1 -> tonydev_v1
```

# override files with previous history
1. git rm file
2. git add file
3. git commit file
4. git push origin
5. git tag
6. git push --tag

```
tony@tony-ST50:~/gerrit_readme/git_local_test/test_v4$ git rm * 
rm 'gerrit_push-readme.txt'
rm 'gerrit_readme.txt'

tony@tony-ST50:~/gerrit_readme/git_local_test/test_v4$ cp ../../*.sh
cp: 在 '../../push_head_tag.sh' 後缺少了要操作的目標檔案
請嘗試執行「cp --help」取得更多訊息。
tony@tony-ST50:~/gerrit_readme/git_local_test/test_v4$ ls
tony@tony-ST50:~/gerrit_readme/git_local_test/test_v4$ cp ../../*.sh .
tony@tony-ST50:~/gerrit_readme/git_local_test/test_v4$ ls
push_head_tag.sh
tony@tony-ST50:~/gerrit_readme/git_local_test/test_v4$ git add .
tony@tony-ST50:~/gerrit_readme/git_local_test/test_v4$ git commit -m "add sh file"
[master dcd542d] add sh file
 3 files changed, 14 insertions(+), 164 deletions(-)
 delete mode 100644 gerrit_push-readme.txt
 delete mode 100644 gerrit_readme.txt
 create mode 100644 push_head_tag.sh
tony@tony-ST50:~/gerrit_readme/git_local_test/test_v4$ ls
push_head_tag.sh
tony@tony-ST50:~/gerrit_readme/git_local_test/test_v4$ git push origin
枚舉物件: 4, 完成.
物件計數中: 100% (4/4), 完成.
使用 12 個執行緒進行壓縮
壓縮物件中: 100% (2/2), 完成.
寫入物件中: 100% (3/3), 557 位元組 | 557.00 KiB/s, 完成.
總共 3 （差異 0），復用 0 （差異 0）
To /home/tony/gerrit_readme/git_local_test/test.git/
   d568729..dcd542d  master -> master

tony@tony-ST50:~/gerrit_readme/git_local_test/test_v4$ git tag v5

tony@tony-ST50:~/gerrit_readme/git_local_test/test_v4$ git push --tag
總共 0 （差異 0），復用 0 （差異 0）
To /home/tony/gerrit_readme/git_local_test/test.git/
 * [new tag]         v5 -> v5
```

# remote sync alternative
- git remote update
- git rebase origin/master
- Note
  - git remote update
    will update all of your branches set to track remote ones, but not merge any changes in.
  - git fetch 
    will update only the branch you're on, but not merge any changes in.
  - git pull  --> merge
    will update and merge any remote changes of the current branch you're on. This would be the one you use to update a local branch.

```
tony@tony-ST50:~/gerrit_readme/git_local_test/test_v3$ ls
gerrit_push-readme.txt  gerrit_readme.txt
tony@tony-ST50:~/gerrit_readme/git_local_test/test_v3$ git remote update
正在取得 origin
remote: 枚舉物件: 9, 完成.
remote: 物件計數中: 100% (9/9), 完成.
remote: 壓縮物件中: 100% (3/3), 完成.
remote: 總共 6 （差異 0），復用 0 （差異 0）
展開物件中: 100% (6/6), 791 位元組 | 791.00 KiB/s, 完成.
來自 /home/tony/gerrit_readme/git_local_test/test
   d568729..dcd542d  master     -> origin/master
   1fc516d..c8bb49c  tonydev    -> origin/tonydev
 * [新標籤]          tonydev_v1 -> tonydev_v1
 * [新標籤]          v5         -> v5

tony@tony-ST50:~/gerrit_readme/git_local_test/test_v3$ ls
gerrit_push-readme.txt  gerrit_readme.txt

tony@tony-ST50:~/gerrit_readme/git_local_test/test_v3$ git rebase origin/master
首先，還原開頭指標以便在其上重放您的工作...
快轉 master 到 origin/master。
tony@tony-ST50:~/gerrit_readme/git_local_test/test_v3$ ls
push_head_tag.sh
tony@tony-ST50:~/gerrit_readme/git_local_test/test_v3$ gitk

```

# merge non-related tree

```
tony@tony-ST50:~/gerrit_readme/git_local_test_b/testb_tagtestb1$ git branch
* master
tony@tony-ST50:~/gerrit_readme/git_local_test_b/testb_tagtestb1$ cat .git/config 
[core]
	repositoryformatversion = 0
	filemode = true
	bare = false
	logallrefupdates = true
[remote "origin"]
	url = /home/tony/gerrit_readme/git_local_test_b/testb.git/
	fetch = +refs/heads/*:refs/remotes/origin/*
[branch "master"]
	remote = origin
	merge = refs/heads/master
tony@tony-ST50:~/gerrit_readme/git_local_test_b/testb_tagtestb1$ git remote add -f test_a ../../git_local_test/test.git/
更新 test_a 中
warning: 沒有共同的提交
remote: 枚舉物件: 19, 完成.
remote: 物件計數中: 100% (19/19), 完成.
remote: 壓縮物件中: 100% (10/10), 完成.
remote: 總共 19 （差異 1），復用 0 （差異 0）
展開物件中: 100% (19/19), 3.67 KiB | 3.67 MiB/s, 完成.
來自 ../../git_local_test/test
 * [新分支]          master     -> test_a/master
 * [新分支]          test1      -> test_a/test1
 * [新分支]          testv3     -> test_a/testv3
 * [新分支]          tonydev    -> test_a/tonydev
 * [新標籤]          tonydev_v1 -> tonydev_v1
 * [新標籤]          v1         -> v1
 * [新標籤]          v3         -> v3
 * [新標籤]          v5         -> v5
 * [新標籤]          testv4     -> testv4
 * [新標籤]          v2         -> v2
tony@tony-ST50:~/gerrit_readme/git_local_test_b/testb_tagtestb1$ cat .git/config 
[core]
	repositoryformatversion = 0
	filemode = true
	bare = false
	logallrefupdates = true
[remote "origin"]
	url = /home/tony/gerrit_readme/git_local_test_b/testb.git/
	fetch = +refs/heads/*:refs/remotes/origin/*
[branch "master"]
	remote = origin
	merge = refs/heads/master
[remote "test_a"]
	url = ../../git_local_test/test.git/
	fetch = +refs/heads/*:refs/remotes/test_a/*
tony@tony-ST50:~/gerrit_readme/git_local_test_b/testb_tagtestb1$ git merge test_a/master
fatal: 拒絕合併無關的歷史

tony@tony-ST50:~/gerrit_readme/git_local_test_b/testb_tagtestb1$ git merge test_a/master --allow-unrelated-histories
Merge made by the 'recursive' strategy.
 push_head_tag.sh | 14 ++++++++++++++
 1 file changed, 14 insertions(+)
 create mode 100644 push_head_tag.sh

tony@tony-ST50:~/gerrit_readme/git_local_test_b/testb_tagtestb1$ ls
push_head_tag.sh  testb.txt

tony@tony-ST50:~/gerrit_readme/git_local_test_b/testb_tagtestb1$ git tag
testb1
testv4
tonydev_v1
v1
v2
v3
v5
```

# rebase non-related tree
```
tony@tony-ST50:~/gerrit_readme/git_local_test_b/testb_tagtestb1$ git remote add -f test_a ../../git_local_test/test.git/
更新 test_a 中
warning: 沒有共同的提交
remote: 枚舉物件: 19, 完成.
remote: 物件計數中: 100% (19/19), 完成.
remote: 壓縮物件中: 100% (10/10), 完成.
remote: 總共 19 （差異 1），復用 0 （差異 0）
展開物件中: 100% (19/19), 3.67 KiB | 3.67 MiB/s, 完成.
來自 ../../git_local_test/test
 * [新分支]          master     -> test_a/master
 * [新分支]          test1      -> test_a/test1
 * [新分支]          testv3     -> test_a/testv3
 * [新分支]          tonydev    -> test_a/tonydev
 * [新標籤]          tonydev_v1 -> tonydev_v1
 * [新標籤]          v1         -> v1
 * [新標籤]          v3         -> v3
 * [新標籤]          v5         -> v5
 * [新標籤]          testv4     -> testv4
 * [新標籤]          v2         -> v2
tony@tony-ST50:~/gerrit_readme/git_local_test_b/testb_tagtestb1$ cat .git/config 
[core]
	repositoryformatversion = 0
	filemode = true
	bare = false
	logallrefupdates = true
[remote "origin"]
	url = /home/tony/gerrit_readme/git_local_test_b/testb.git/
	fetch = +refs/heads/*:refs/remotes/origin/*
[branch "master"]
	remote = origin
	merge = refs/heads/master
[remote "test_a"]
	url = ../../git_local_test/test.git/
	fetch = +refs/heads/*:refs/remotes/test_a/*
tony@tony-ST50:~/gerrit_readme/git_local_test_b/testb_tagtestb1$ gitk
tony@tony-ST50:~/gerrit_readme/git_local_test_b/testb_tagtestb1$ git rebase test_a/master
首先，還原開頭指標以便在其上重放您的工作...
應用：testb: testb1

tony@tony-ST50:~/gerrit_readme/git_local_test_b/testb_tagtestb1$ ls
push_head_tag.sh  testb.txt


tony@tony-ST50:~/gerrit_readme/git_local_test_b/testb_tagtestb1$ git push origin
To /home/tony/gerrit_readme/git_local_test_b/testb.git/
 ! [rejected]        master -> master (non-fast-forward)
error: 推送一些引用到 '/home/tony/gerrit_readme/git_local_test_b/testb.git/' 失敗
提示：更新被拒絕，因為您目前分支的最新提交落後於其對應的遠端分支。
提示：再次推送前，先與遠端變更合併（如 'git pull ...'）。詳見
提示：'git push --help' 中的 'Note about fast-forwards' 小節。

tony@tony-ST50:~/gerrit_readme/git_local_test_b/testb_tagtestb1$ git pull
fatal: 拒絕合併無關的歷史
tony@tony-ST50:~/gerrit_readme/git_local_test_b/testb_tagtestb1$ git pull --allow-unrelated-histories
Merge made by the 'recursive' strategy.


tony@tony-ST50:~/gerrit_readme/git_local_test_b/testb_tagtestb1$ ls
push_head_tag.sh  testb.txt
tony@tony-ST50:~/gerrit_readme/git_local_test_b/testb_tagtestb1$ git push origin
枚舉物件: 20, 完成.
物件計數中: 100% (20/20), 完成.
使用 12 個執行緒進行壓縮
壓縮物件中: 100% (12/12), 完成.
寫入物件中: 100% (19/19), 3.90 KiB | 3.90 MiB/s, 完成.
總共 19 （差異 1），復用 0 （差異 0）
To /home/tony/gerrit_readme/git_local_test_b/testb.git/
   2a2aba8..68a2a0b  master -> master

tony@tony-ST50:~/gerrit_readme/git_local_test_b/testb_tagtestb1$ cd ..
tony@tony-ST50:~/gerrit_readme/git_local_test_b$ git clone testb.git/ testb_rebase
正複製到 'testb_rebase'...
完成。
tony@tony-ST50:~/gerrit_readme/git_local_test_b$ cd testb_rebase/
tony@tony-ST50:~/gerrit_readme/git_local_test_b/testb_rebase$ git tag
testb1


tony@tony-ST50:~/gerrit_readme/git_local_test_b/testb_rebase$ cd ..
tony@tony-ST50:~/gerrit_readme/git_local_test_b$ cd testb_tagtestb1/
tony@tony-ST50:~/gerrit_readme/git_local_test_b/testb_tagtestb1$ git push --tag
枚舉物件: 5, 完成.
物件計數中: 100% (5/5), 完成.
寫入物件中: 100% (3/3), 286 位元組 | 286.00 KiB/s, 完成.
總共 3 （差異 0），復用 0 （差異 0）
To /home/tony/gerrit_readme/git_local_test_b/testb.git/
 * [new tag]         testv4 -> testv4
 * [new tag]         tonydev_v1 -> tonydev_v1
 * [new tag]         v1 -> v1
 * [new tag]         v2 -> v2
 * [new tag]         v3 -> v3
 * [new tag]         v5 -> v5
tony@tony-ST50:~/gerrit_readme/git_local_test_b/testb_tagtestb1$ cd ..
tony@tony-ST50:~/gerrit_readme/git_local_test_b$ git clone testb.git/ testb_rebase_tag
正複製到 'testb_rebase_tag'...
完成。

tony@tony-ST50:~/gerrit_readme/git_local_test_b$ cd testb_tagtestb1/
tony@tony-ST50:~/gerrit_readme/git_local_test_b/testb_tagtestb1$ git tag
testb1
testv4
tonydev_v1
v1
v2
v3
v5
```

