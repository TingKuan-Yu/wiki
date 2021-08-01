11:28 PM
@Mark 請教一下, 原來我GKI PR可merge但後來conflict, 應怎麼處理好, 是退掉重上嗎?

10.4是否已上main? by Tony Yu
Tony Yu11:28 PM
10.4是否已上main?

Profile picture of Mark Hsu.rebase by Mark Hsu
Mark Hsu
11:28 PM
rebase
對 by Mark Hsu
Mark Hsu11:29 PM
對
不過你現在還能pull嗎 by Mark Hsu
Mark Hsu11:29 PM
不過你現在還能pull嗎
commit都不一樣 by Mark Hsu
Mark Hsu11:29 PM
commit都不一樣
就一整個不知怎麼處理, 想說重上. by Tony Yu
Tony Yu
11:30 PM
就一整個不知怎麼處理, 想說重上.

Profile picture of Amy Tang.你先git format-patch by Amy Tang
Amy Tang
11:30 PM
你先git format-patch

自己建Patch by Amy Tang
Amy Tang11:30 PM
Edited
自己建Patch

然後切branch 把c1/11/main刪掉 by Amy Tang
Amy Tang11:30 PM
然後切branch 把c1/11/main刪掉

在git fetch下來 by Amy Tang
Amy Tang11:30 PM
在git fetch下來

Profile picture of Mark Hsu.你先看看能不能pull最新的 然後你的branch rebase by Mark Hsu
Mark Hsu
11:30 PM
你先看看能不能pull最新的 然後你的branch rebase
Profile picture of Amy Tang.再切過去重打 by Amy Tang
Amy Tang
11:30 PM
再切過去重打

Profile picture of Mark Hsu.不行的話就要像amy說的 by Mark Hsu

Mark Hsu
11:31 PM
不行的話就要像amy說的
應該 很大可能不行 by Mark Hsu

Mark Hsu11:31 PM
應該 很大可能不行
明天來試rebase看看, 若解不了conflict, 只好重上看看. by Tony Yu

Tony Yu
11:32 PM
明天來試rebase看看, 若解不了conflict, 只好重上看看.

謝了. by Tony Yu

Tony Yu11:32 PM
謝了.

Profile picture of Mark Hsu.把你改的變成patch 重建打進去 就像amy說的 比較快 by Mark Hsu

Mark Hsu
11:33 PM
把你改的變成patch 重建打進去 就像amy說的 比較快
那pr會變新的. by Tony Yu

Tony Yu
11:33 PM
那pr會變新的.

又要重加 by Tony Yu

Tony Yu11:33 PM
又要重加

Profile picture of Amy Tang.你可以force push by Amy Tang

Amy Tang
11:33 PM
你可以force push

你打完以後 先刪掉local舊的branch by Amy Tang

Amy Tang11:34 PM
你打完以後 先刪掉local舊的branch

在建一個一樣名稱的 by Amy Tang

Amy Tang11:34 PM
在建一個一樣名稱的

然後force-push by Amy Tang

Amy Tang11:34 PM
然後force-push

就會是同一個PR了 by Amy Tang

Amy Tang11:34 PM
👍
1
就會是同一個PR了

真的? 好的. 明天來試force-push 都一branch . by Tony Yu

Tony Yu
11:35 PM
真的? 好的. 明天來試force-push 都一branch .



