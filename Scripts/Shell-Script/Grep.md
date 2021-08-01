

# Find pattern recursively in current folder 
- https://codertw.com/%E7%A8%8B%E5%BC%8F%E8%AA%9E%E8%A8%80/424418/#outline__1_1_1 
```
grep "main()" . -r --include *.{php,html}
grep "main()" . -r --exclude "README"
grep "main()" . -r --exclude-from filelist
```