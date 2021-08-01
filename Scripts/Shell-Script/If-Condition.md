# reference
- http://linux.vbird.org/linux_basic/0340bashshell-scripts.php#rule

# 12.3 善用判斷式
在第十章中，我們提到過 $? 這個變數所代表的意義， 此外，也透過 && 及 || 來作為前一個指令執行回傳值對於後一個指令是否要進行的依據。第十章的討論中，如果想要判斷一個目錄是否存在， 當時我們使用的是 ls 這個指令搭配資料流重導向，最後配合 $? 來決定後續的指令進行與否。 但是否有更簡單的方式可以來進行『條件判斷』呢？有的～那就是『 test 』這個指令。


## 12.3.1 利用 test 指令的測試功能
當我要檢測系統上面某些檔案或者是相關的屬性時，利用 test 這個指令來工作真是好用得不得了， 舉例來說，我要檢查 /dmtsai 是否存在時，使用：

[dmtsai@study ~]$ test -e /dmtsai
執行結果並不會顯示任何訊息，但最後我們可以透過 $? 或 && 及 || 來展現整個結果呢！ 例如我們在將上面的例子改寫成這樣：

[dmtsai@study ~]$ test -e /dmtsai && echo "exist" || echo "Not exist"
Not exist  <==結果顯示不存在啊！
最終的結果可以告知我們是『exist』還是『Not exist』呢！那我知道 -e 是測試一個『東西』在不在， 如果還想要測試一下該檔名是啥玩意兒時，還有哪些標誌可以來判斷的呢？呵呵！有底下這些東西喔！

測試的標誌	代表意義
### 1. 關於某個檔名的『檔案類型』判斷，如 test -e filename 表示存在否
-e	該『檔名』是否存在？(常用)
-f	該『檔名』是否存在且為檔案(file)？(常用)
-d	該『檔名』是否存在且為目錄(directory)？(常用)
-b	該『檔名』是否存在且為一個 block device 裝置？
-c	該『檔名』是否存在且為一個 character device 裝置？
-S	該『檔名』是否存在且為一個 Socket 檔案？
-p	該『檔名』是否存在且為一個 FIFO (pipe) 檔案？
-L	該『檔名』是否存在且為一個連結檔？
### 2. 關於檔案的權限偵測，如 test -r filename 表示可讀否 (但 root 權限常有例外)
-r	偵測該檔名是否存在且具有『可讀』的權限？
-w	偵測該檔名是否存在且具有『可寫』的權限？
-x	偵測該檔名是否存在且具有『可執行』的權限？
-u	偵測該檔名是否存在且具有『SUID』的屬性？
-g	偵測該檔名是否存在且具有『SGID』的屬性？
-k	偵測該檔名是否存在且具有『Sticky bit』的屬性？
-s	偵測該檔名是否存在且為『非空白檔案』？
### 3. 兩個檔案之間的比較，如： test file1 -nt file2
-nt	(newer than)判斷 file1 是否比 file2 新
-ot	(older than)判斷 file1 是否比 file2 舊
-ef	判斷 file1 與 file2 是否為同一檔案，可用在判斷 hard link 的判定上。 主要意義在判定，兩個檔案是否均指向同一個 inode 哩！
### 4. 關於兩個整數之間的判定，例如 test n1 -eq n2
-eq	兩數值相等 (equal)
-ne	兩數值不等 (not equal)
-gt	n1 大於 n2 (greater than)
-lt	n1 小於 n2 (less than)
-ge	n1 大於等於 n2 (greater than or equal)
-le	n1 小於等於 n2 (less than or equal)
### 5. 判定字串的資料
test -z string	判定字串是否為 0 ？若 string 為空字串，則為 true
test -n string	判定字串是否非為 0 ？若 string 為空字串，則為 false。
註： -n 亦可省略
test str1 == str2	判定 str1 是否等於 str2 ，若相等，則回傳 true
test str1 != str2	判定 str1 是否不等於 str2 ，若相等，則回傳 false
6. 多重條件判定，例如： test -r filename -a -x filename
-a	(and)兩狀況同時成立！例如 test -r file -a -x file，則 file 同時具有 r 與 x 權限時，才回傳 true。
-o	(or)兩狀況任何一個成立！例如 test -r file -o -x file，則 file 具有 r 或 x 權限時，就可回傳 true。
!	反相狀態，如 test ! -x file ，當 file 不具有 x 時，回傳 true
