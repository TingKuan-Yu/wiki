[[_TOC_]]


# git general operation
- git format-patch
```
count=`git rev-list <base commit id>..latest commit id> --count`
git format-patch -o output_patch -$count
```
- git am
- git am 000x....patch
- Note: git am output_patch/*.patch could be work

# Fix conflict of git am 
## add all conflict files, use "git add", and use "git am --continue"
- apply patch
```
tony@UbuntM-VB:~/git_repo_test/git_conflict_test/gitrepo$ echo conflict_test > code.cpp 
tony@UbuntM-VB:~/git_repo_test/git_conflict_test/gitrepo$ git add .
tony@UbuntM-VB:~/git_repo_test/git_conflict_test/gitrepo$ git commit -m "set to conflict_test"
[conflicttest c2eeb8b] set to conflict_test
 1 file changed, 1 insertion(+), 5 deletions(-)

tony@UbuntM-VB:~/git_repo_test/git_conflict_test/gitrepo$ git am ../patches/0001-add-cde.patch
Applying: add cde
error: code.cpp: already exists in index
Patch failed at 0001 add cde
Use 'git am --show-current-patch' to see the failed patch
When you have resolved this problem, run "git am --continue".
If you prefer to skip this patch, run "git am --skip" instead.
To restore the original branch and stop patching, run "git am --abort".

tony@UbuntM-VB:~/git_repo_test/git_conflict_test/gitrepo$ git am --show-current-patch
From 7f4dd0d4a1049597abf92ba266dd86363afc323a Mon Sep 17 00:00:00 2001
From: Tony Yu <tingkuanyu@microsoft.com>
Date: Wed, 21 Apr 2021 17:39:58 +0800
Subject: [PATCH 1/2] add cde

---
 code.cpp | 2 ++
 1 file changed, 2 insertions(+)
 create mode 100644 code.cpp

diff --git a/code.cpp b/code.cpp
new file mode 100644
index 0000000..2a49fe2
--- /dev/null
+++ b/code.cpp
@@ -0,0 +1,2 @@
+abc
+cde
-- 
2.17.1
tony@UbuntM-VB:~/git_repo_test/git_conflict_test/gitrepo$ cat code.cpp 
conflict_test
```
- Use vim or other editors to modify code.cpp to generate new code.cpp
- Now, we can add code.cpp and continue the patch.
```
tony@UbuntM-VB:~/git_repo_test/git_conflict_test/gitrepo$ git add .
tony@UbuntM-VB:~/git_repo_test/git_conflict_test/gitrepo$ git am --continue
Applying: add cde

```

## use --reject method
```
tony@UbuntM-VB:~/git_repo_test/git_conflict_test/gitrepo$ git branch
* conflicttest
  master
tony@UbuntM-VB:~/git_repo_test/git_conflict_test/gitrepo$ git checkout master
Switched to branch 'master'
tony@UbuntM-VB:~/git_repo_test/git_conflict_test/gitrepo$ ls
code.cpp
tony@UbuntM-VB:~/git_repo_test/git_conflict_test/gitrepo$ echo tony >> code.cpp
tony@UbuntM-VB:~/git_repo_test/git_conflict_test/gitrepo$ git add .
tony@UbuntM-VB:~/git_repo_test/git_conflict_test/gitrepo$ git commit -m "add tony"
[master 7ed8145] add tony
 1 file changed, 1 insertion(+)

tony@UbuntM-VB:~/git_repo_test/git_conflict_test/gitrepo$ git format-patch -n1 -o ../
../0001-add-tony.patch
tony@UbuntM-VB:~/git_repo_test/git_conflict_test/gitrepo$ git branch
  conflicttest
* master
tony@UbuntM-VB:~/git_repo_test/git_conflict_test/gitrepo$ git checkout conflicttest 
Switched to branch 'conflicttest'

tony@UbuntM-VB:~/git_repo_test/git_conflict_test/gitrepo$ git am ../0001-add-tony.patch
Applying: add tony
error: patch failed: code.cpp:3
error: code.cpp: patch does not apply
Patch failed at 0001 add tony
Use 'git am --show-current-patch' to see the failed patch
When you have resolved this problem, run "git am --continue".
If you prefer to skip this patch, run "git am --skip" instead.
To restore the original branch and stop patching, run "git am --abort".
tony@UbuntM-VB:~/git_repo_test/git_conflict_test/gitrepo$ git apply --reject .git/rebase-apply/0001
Checking patch code.cpp...
error: while searching for:
cde
def
ghi

error: patch failed: code.cpp:3
Applying patch code.cpp with 1 reject...
Rejected hunk #1.
tony@UbuntM-VB:~/git_repo_test/git_conflict_test/gitrepo$ ls
code.cpp  code.cpp.rej

tony@UbuntM-VB:~/git_repo_test/git_conflict_test/gitrepo$ cat code.cpp.rej 
diff a/code.cpp b/code.cpp	(rejected hunks)
@@ -3,3 +3,4 @@ cde
 cde
 def
 ghi
+tony
tony@UbuntM-VB:~/git_repo_test/git_conflict_test/gitrepo$ cat code.cpp
conflict_test
abc
cde

tony@UbuntM-VB:~/git_repo_test/git_conflict_test/gitrepo$ echo tony >> code.cpp
tony@UbuntM-VB:~/git_repo_test/git_conflict_test/gitrepo$ rm code.cpp.rej 
tony@UbuntM-VB:~/git_repo_test/git_conflict_test/gitrepo$ git add code.cpp 
tony@UbuntM-VB:~/git_repo_test/git_conflict_test/gitrepo$ git am --resolved
Applying: add tony
```

## use three way method
```
tony@UbuntM-VB:~/git_repo_test/git_conflict_test/gitrepo$ git branch
* conflicttest
  master
tony@UbuntM-VB:~/git_repo_test/git_conflict_test/gitrepo$ git checkout master
Switched to branch 'master'
tony@UbuntM-VB:~/git_repo_test/git_conflict_test/gitrepo$ echo "three way" > code.cpp 
tony@UbuntM-VB:~/git_repo_test/git_conflict_test/gitrepo$ git add .
tony@UbuntM-VB:~/git_repo_test/git_conflict_test/gitrepo$ git commit -m "only three way"
[master 31c51b9] only three way
 1 file changed, 6 deletions(-)
tony@UbuntM-VB:~/git_repo_test/git_conflict_test/gitrepo$ git format-patch -n1 -o ../
../0001-only-three-way.patch

tony@UbuntM-VB:~/git_repo_test/git_conflict_test/gitrepo$ git checkout conflicttest 
Switched to branch 'conflicttest'
tony@UbuntM-VB:~/git_repo_test/git_conflict_test/gitrepo$ git am ../0001-only-three-way.patch
Applying: only three way
error: patch failed: code.cpp:1
error: code.cpp: patch does not apply
Patch failed at 0001 only three way
Use 'git am --show-current-patch' to see the failed patch
When you have resolved this problem, run "git am --continue".
If you prefer to skip this patch, run "git am --skip" instead.
To restore the original branch and stop patching, run "git am --abort".
tony@UbuntM-VB:~/git_repo_test/git_conflict_test/gitrepo$ git am --3way
Applying: only three way
Using index info to reconstruct a base tree...
M	code.cpp
Falling back to patching base and 3-way merge...
Auto-merging code.cpp
CONFLICT (content): Merge conflict in code.cpp
error: Failed to merge in the changes.
Patch failed at 0001 only three way
Use 'git am --show-current-patch' to see the failed patch
When you have resolved this problem, run "git am --continue".
If you prefer to skip this patch, run "git am --skip" instead.
To restore the original branch and stop patching, run "git am --abort".

tony@UbuntM-VB:~/git_repo_test/git_conflict_test/gitrepo$ cat code.cpp 
<<<<<<< HEAD
conflict_test
abc
cde
tony
=======
>>>>>>> only three way
three way
tony@UbuntM-VB:~/git_repo_test/git_conflict_test/gitrepo$ vim code.cpp 
tony@UbuntM-VB:~/git_repo_test/git_conflict_test/gitrepo$ cat code.cpp 
three way
tony@UbuntM-VB:~/git_repo_test/git_conflict_test/gitrepo$ git add code.cpp 
tony@UbuntM-VB:~/git_repo_test/git_conflict_test/gitrepo$ git am --resolved 
Applying: only three way
```