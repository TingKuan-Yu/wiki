# git push specific commit to remot
- https://dev.azure.com/E-OS/device/_git/device.config/commit/366bb6c92490e990dd586e102a5687e466ed2e4b?refName=refs%2Fheads%2Fpersonal%2Ftony%2Fgki_task171871
- it push device 366bb6c:**refs/heads**/personal/tony/gki_task171871
```
tingkuanyu@TonyYuLinux1:/D/c1/11/main/kernel-gki-phase1/device_build$ git push device 366bb6c:refs/heads/personal/tony/gki_task171871
Enumerating objects: 7, done.
Counting objects: 100% (7/7), done.
Delta compression using up to 20 threads
Compressing objects: 100% (4/4), done.
Writing objects: 100% (4/4), 929 bytes | 929.00 KiB/s, done.
Total 4 (delta 2), reused 0 (delta 0)
remote: Analyzing objects... (4/4) (11 ms)
remote: Checking for credentials and other secrets... (1/1) done (49 ms)
remote: Storing packfile... done (91 ms)
remote: Storing index... done (53 ms)
To ssh://ssh.dev.azure.com/v3/e-os/device/device.config
 * [new branch]      366bb6c -> personal/tony/gki_task171871
```