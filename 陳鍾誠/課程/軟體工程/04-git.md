## 第 4 章 -- Git 合作

Git 是很好用的版本管理系統，而 Github 則是 Git 的專案大倉庫，包含了全世界的開放原始碼專案，我們可以透過 Git + Github 將專案發布在網路上，讓全世界的人都可以看到你的作品。

另外、我們可以透過 Git + Github 進行專案下載、修改、測試、發佈的動作，只要使用 git clone 就可以下載專案，然後修改測試完畢之後，再用 git add -A; git commit -m "xxxx"; git push origin master 就能將專案推回 github 上。

對於兩人以上的專案，我們可以採用 Git + Github 進行合作，合作的方式有很多種，以下是常見的幾種：

1. 使用 fork + pull request 的方式進行協作
2. 將開發成員加入 collaborator ，然後用 git branch 的方式開發分支版本，完成後再合併回 master

在本章中，我們將先學習 github 的用法，然後再學習使用 fork + pull request 的合作方法。

### Git + Github 的基本使用方式

首先我們先學習如何創建 github 專案。

先在 github 右上角的 + 按鈕上點一下，新增一個專案 (例如 zlodash)，然後在你的命令列中執行下列指令:

```
PS D:\course\sejs\project> mkdir zlodash


    目錄: D:\course\sejs\project


Mode                LastWriteTime         Length Name
----                -------------         ------ ----
d-----      2018/11/3  上午 09:31                zlodash


PS D:\course\sejs\project> cd zlodash
PS D:\course\sejs\project\zlodash> git init
Initialized empty Git repository in D:/course/sejs/project/zlodash/.git/
```

接著您可以把專案檔加入到該資料夾檔案中 (複製或撰寫)，在確定專案測試 ok 之後，應該先進行測試，如以下範例所示：

```
PS D:\course\sejs\project\zlodash> npm run test
npm WARN npm npm does not support Node.js v11.0.0
npm WARN npm You should probably upgrade to a newer version of node as we
npm WARN npm can't make any promises that npm will work with this version.
npm WARN npm Supported releases of Node.js are the latest release of 4, 6, 7, 8, 9.
npm WARN npm You can find the latest version at https://nodejs.org/

> ccclodash@0.4.0 test D:\course\sejs\project\zlodash
> mocha



  chunk
    √ _.chunk(['a', 'b', 'c', 'd'], 2) equalTo [ [ 'a', 'b' ], [ 'c', 'd' ] ]
    √ _.chunk(['a', 'b', 'c', 'd'], 3) equalTo [ [ 'a', 'b', 'c' ], [ 'd' ] ]
    √ _.chunk(['a', 'b', 'c', 'd'], 3) notEqualTo [ [ 'a', 'b'], ['c' , 'd' ] ]

  compact
    √ _.compact([0, 1, false, 2, '', 3]) equalTo [ 1, 2, 3 ]

  concat
    √ concat(array, 2, [3], [[4]]) equalTo [1, 2, [3], [[4]]]
    √ concat(array, ....) will not modify array

  flattenDeep
    √ flattenDeep([1, [2, [3, [4]], 5]]) => [1, 2, 3, 4, 5]


  7 passing (64ms)
```

然後你就可以執行下列動作將該專案上傳到 github 上。

```
$ git add -A
$ git commit -m "xxxx"
$ git remote add origin 你的專案網址
$ git push origin master
```

以下是我操作的過程：

```
PS D:\course\sejs\project\zlodash> git add -A
warning: LF will be replaced by CRLF in package-lock.json.
The file will have its original line endings in your working directory.
warning: LF will be replaced by CRLF in package.json.
The file will have its original line endings in your working directory.
PS D:\course\sejs\project\zlodash> git commit -m "init and first commit"
[master (root-commit) f859fe6] init and first commit
 35 files changed, 8806 insertions(+)
 create mode 100644 .gitignore
 create mode 100644 .travis.yml
 create mode 100644 LICENSE
 create mode 100644 README.md
 create mode 100644 dist/ccclodash.js
 create mode 100644 dist/index.html
 create mode 100644 dist/pub.js
 create mode 100644 docs/-_.html
 create mode 100644 docs/index.html
 create mode 100644 docs/index.js.html
 create mode 100644 docs/lib_chunk.js.html
 create mode 100644 docs/lib_compact.js.html
 create mode 100644 docs/lib_concat.js.html
 create mode 100644 docs/scripts/collapse.js
 create mode 100644 docs/scripts/jquery-3.1.1.min.js
 create mode 100644 docs/scripts/linenumber.js
 create mode 100644 docs/scripts/prettify/Apache-License-2.0.txt
 create mode 100644 docs/scripts/prettify/lang-css.js
 create mode 100644 docs/scripts/prettify/prettify.js
 create mode 100644 docs/scripts/search.js
 create mode 100644 docs/styles/jsdoc.css
 create mode 100644 docs/styles/prettify.css
 create mode 100644 example/chunkEx.js
 create mode 100644 index.js
 create mode 100644 lib/chunk.js
 create mode 100644 lib/compact.js
 create mode 100644 lib/concat.js
 create mode 100644 lib/flattenDeep.js
 create mode 100644 md/jsdoc.md
 create mode 100644 package-lock.json
 create mode 100644 package.json
 create mode 100644 test/chunkTest.js
 create mode 100644 test/compactTest.js
 create mode 100644 test/concatTest.js
 create mode 100644 test/flattenTest.js
PS D:\course\sejs\project\zlodash> npm i
npm WARN npm npm does not support Node.js v11.0.0
npm WARN npm You should probably upgrade to a newer version of node as we
npm WARN npm can't make any promises that npm will work with this version.
npm WARN npm Supported releases of Node.js are the latest release of 4, 6, 7, 8, 9.
npm WARN npm You can find the latest version at https://nodejs.org/

> husky@1.1.1 install D:\course\sejs\project\zlodash\node_modules\husky
> node husky install

husky > setting up git hooks
husky > done
added 705 packages in 105.493s
PS D:\course\sejs\project\zlodash> git remote add origin https://github.com/se107a/zlodash.git
PS D:\course\sejs\project\zlodash> git push origin master
fatal: HttpRequestException encountered.
   傳送要求時發生錯誤。
Username for 'https://github.com': ccckmit
Password for 'https://ccckmit@github.com':
Counting objects: 46, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (42/42), done.
Writing objects: 100% (46/46), 100.06 KiB | 1.59 MiB/s, done.
Total 46 (delta 4), reused 0 (delta 0)
remote: Resolving deltas: 100% (4/4), done.
remote:
remote: Create a pull request for 'master' on GitHub by visiting:
remote:      https://github.com/se107a/zlodash/pull/new/master
remote:
To https://github.com/se107a/zlodash.git
 * [new branch]      master -> master
```

這樣您應該就完成了第一個 github 專案的創建動作。

### 兩人合作 (一人分飾兩角)

接著我們來學習如何用 github 進行合作，為了能夠全面理解，我們先用《一人分飾兩角》的方式，自己和自己進行合作：

首先貢獻者必須先 fork 該專案之後，開始修改程式並加入新函數，加好之後先進行測試：

```
PS D:\course\ccckmit\ccclodash> mocha


  chunk
    √ _.chunk(['a', 'b', 'c', 'd'], 2) equalTo [ [ 'a', 'b' ], [ 'c', 'd' ] ] (79ms)
    √ _.chunk(['a', 'b', 'c', 'd'], 3) equalTo [ [ 'a', 'b', 'c' ], [ 'd' ] ]
    √ _.chunk(['a', 'b', 'c', 'd'], 3) notEqualTo [ [ 'a', 'b'], ['c' , 'd' ] ]

  compact
    √ _.compact([0, 1, false, 2, '', 3]) equalTo [ 1, 2, 3 ]

  concat
    √ _.concat(array, 2, [3], [[4]]) equalTo [1, 2, [3], [[4]]]
    √ _.concat(array, 2, [3], [[4]]) equalTo [ 1, 2, 3 ]

  flattenDeep
    √ flattenDeep([1, [2, [3, [4]], 5]]) => [1, 2, 3, 4, 5]


  7 passing (157ms)
```

測試完畢沒問題後，就可以上傳到自己 fork 的專案上：

```
PS D:\course\ccckmit\ccclodash> git add -A
PS D:\course\ccckmit\ccclodash> git commit -m "finished flattenDeep()"
husky > pre-commit (node v10.11.0)
25lRunning tasks for lib/*.js [started]
prettier --write [started]
prettier --write [completed]
git add [started]
git add [completed]
Running tasks for lib/*.js [completed]
25h25h[master ecd8601] finished flattenDeep()
 3 files changed, 41 insertions(+), 1 deletion(-)
 create mode 100644 lib/flattenDeep.js
 create mode 100644 test/flattenTest.js
PS D:\course\ccckmit\ccclodash> git push origin master
fatal: HttpRequestException encountered.
   傳送要求時發生錯誤。
Username for 'https://github.com': ccckmit
Password for 'https://ccckmit@github.com':
Counting objects: 9, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (9/9), done.
Writing objects: 100% (9/9), 1.91 KiB | 391.00 KiB/s, done.
Total 9 (delta 4), reused 0 (delta 0)
remote: Resolving deltas: 100% (4/4), completed with 4 local objects.
To https://github.com/ccckmit/ccclodash.git
   46a67a5..ecd8601  master -> master
```

接著在 github 的 fork 專案上按下 pull request 鈕，告訴主導者，你 (貢獻者) 已經修改了一個版本，請主導者來收取。

### 主導者測試並納入專案

然後主導者必須先確定貢獻者版本的正確性，因此必須先使用 fetch 將該貢獻版本抓下來到一個新的 branch 版本 (以下範例中的 ccckmitFlattenDeep) ，然後將 master 與該版本合併後進行測試。(這樣才能確認合併後的版本是沒問題的)

```
PS D:\course\se107a\example\ccclodash> git remote add ccckmit https://github.com/ccckmit/ccclodash.git
PS D:\course\se107a\example\ccclodash> git fetch ccckmit
remote: Enumerating objects: 21, done.
remote: Counting objects: 100% (21/21), done.
remote: Compressing objects: 100% (7/7), done.
remote: Total 14 (delta 8), reused 13 (delta 7), pack-reused 0
Unpacking objects: 100% (14/14), done.
From https://github.com/ccckmit/ccclodash
 * [new branch]      master     -> ccckmit/master
PS D:\course\se107a\example\ccclodash> git checkout -b ccckmitFlattenDeep
Switched to a new branch 'ccckmitFlattenDeep'
M       package-lock.json
M       package.json
PS D:\course\se107a\example\ccclodash> git merge ccckmit/master
error: Your local changes to the following files would be overwritten by merge:
        package-lock.json
        package.json
Please commit your changes or stash them before you merge.
Aborting
Updating f72805d..ecd8601
PS D:\course\se107a\example\ccclodash> git status
On branch ccckmitFlattenDeep
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

        modified:   package-lock.json
        modified:   package.json

no changes added to commit (use "git add" and/or "git commit -a")
PS D:\course\se107a\example\ccclodash> git stash
warning: LF will be replaced by CRLF in package-lock.json.
The file will have its original line endings in your working directory.
warning: LF will be replaced by CRLF in package.json.
The file will have its original line endings in your working directory.
Saved working directory and index state WIP on ccckmitFlattenDeep: f72805d Merge pull request #1 from ccckmit/master
PS D:\course\se107a\example\ccclodash> git merge ccckmit/master
Updating f72805d..ecd8601
Fast-forward
 index.js            |    3 +-
 lib/chunk.js        |   12 +-
 lib/flattenDeep.js  |   30 +
 package-lock.json   | 2111 +++++++++++++++++++++++++++++++++++++++++++++++++--
 package.json        |   25 +-
 test/flattenTest.js |    9 +
 6 files changed, 2110 insertions(+), 80 deletions(-)
 create mode 100644 lib/flattenDeep.js
 create mode 100644 test/flattenTest.js
PS D:\course\se107a\example\ccclodash> mocha


  chunk
    √ _.chunk(['a', 'b', 'c', 'd'], 2) equalTo [ [ 'a', 'b' ], [ 'c', 'd' ] ]
    √ _.chunk(['a', 'b', 'c', 'd'], 3) equalTo [ [ 'a', 'b', 'c' ], [ 'd' ] ]
    √ _.chunk(['a', 'b', 'c', 'd'], 3) notEqualTo [ [ 'a', 'b'], ['c' , 'd' ] ]

  compact
    √ _.compact([0, 1, false, 2, '', 3]) equalTo [ 1, 2, 3 ]

  concat
    √ _.concat(array, 2, [3], [[4]]) equalTo [1, 2, [3], [[4]]]
    √ _.concat(array, 2, [3], [[4]]) equalTo [ 1, 2, 3 ]

  flattenDeep
    √ flattenDeep([1, [2, [3, [4]], 5]]) => [1, 2, 3, 4, 5]


  7 passing (61ms)

PS D:\course\se107a\example\ccclodash> git checkout master
Switched to branch 'master'
Your branch is up to date with 'origin/master'.
PS D:\course\se107a\example\ccclodash> git merge ccckmit/master
Updating f72805d..ecd8601
Fast-forward
 index.js            |    3 +-
 lib/chunk.js        |   12 +-
 lib/flattenDeep.js  |   30 +
 package-lock.json   | 2111 +++++++++++++++++++++++++++++++++++++++++++++++++--
 package.json        |   25 +-
 test/flattenTest.js |    9 +
 6 files changed, 2110 insertions(+), 80 deletions(-)
 create mode 100644 lib/flattenDeep.js
 create mode 100644 test/flattenTest.js
PS D:\course\se107a\example\ccclodash> git diff origin/master
diff --git a/index.js b/index.js
index bcf6688..0c1845f 100644
--- a/index.js
+++ b/index.js
@@ -2,5 +2,6 @@
 module.exports = {
   chunk: require('./lib/chunk'),
   compact: require('./lib/compact'),
-  concat: require('./lib/concat')
+  concat: require('./lib/concat'),
+  flattenDeep: require('./lib/flattenDeep')
 }
```

接著您可以用 npm run test 或者 mocha 之類的指令，確定測試沒問題之後，就可以將這個合併版本，推回 github 上了。

```
PS D:\course\se107a\example\ccclodash> git push origin master
Username for 'https://github.com': ccckmit
Password for 'https://ccckmit@github.com':
Counting objects: 14, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (14/14), done.
Writing objects: 100% (14/14), 17.99 KiB | 1.20 MiB/s, done.
Total 14 (delta 8), reused 0 (delta 0)
remote: Resolving deltas: 100% (8/8), completed with 6 local objects.
To https://github.com/se107a/ccclodash.git
   f72805d..ecd8601  master -> master
```

以上過程展示了透過 github : fork + pull request 進行專案合作的方法，這種方法可以不斷接收新版本，因此也可以有很多貢獻者，所以可以用在兩人或多人合作上，但必須有個主專案。

如果希望更快速的合作，可以採用《不需要 fork, 多人共享一個 git 專案的方式》，方法如下：

1. 將開發成員加入 collaborator ，然後用 git branch 的方式開發分支版本，完成後再合併回 master


### 練習

> 基本參考：https://github.com/cccbook/sejs/tree/master/example/03-npm
> 進階參考: https://github.com/se107a/ccclodash

### 練習 1 -- Github 基礎

1. 延續《上一個練習》在 github 上為你的專案創造一個 repository
2. 修改你的 package.json 欄位，加入 repository 欄位
    * https://github.com/se107a/ccclodash/blob/master/package.json
3. 用 git remote add origin 專案網址 的指令，設定好 origin 網址
    * 參考 ： [Git 基礎 - 與遠端協同工作](https://git-scm.com/book/zh-tw/v1/Git-%E5%9F%BA%E7%A4%8E-%E8%88%87%E9%81%A0%E7%AB%AF%E5%8D%94%E5%90%8C%E5%B7%A5%E4%BD%9C)
4. 用 git add -A, git commit -m 訊息, git push origin master 將套件出版在 github 上。
    *  [Git 基礎 - 與遠端協同工作](https://git-scm.com/book/zh-tw/v1/Git-%E5%9F%BA%E7%A4%8E-%E8%88%87%E9%81%A0%E7%AB%AF%E5%8D%94%E5%90%8C%E5%B7%A5%E4%BD%9C)
5. 再次用 npm publish 發布你的套件，檢查下列網址
    * https://www.npmjs.com/package/你的套件名稱
    * npm 套件的發布常常會延時，要過比較久才看得到，您可以在 yarn 看看該套件是否發布完成
    * (yarn 比較快，算是 npm 的競爭對手 ....)

### 練習 2 -- 雙人合作初體驗 (pull request)

請延續 《上一個練習》，試著用一人分飾兩角的方式，採用 organization + pull request 自己與自己合作！

0. 在 github 中創造一個 organization
    * https://github.com/settings/organizations
1. 在該 organization 上為你的套件開一個專案
    * 參考 ： https://github.com/se107a/ccclodash
2. 將該專案 fork 到自己的身分帳號下 (非 organization)
    * 主導者: https://github.com/se107a/ccclodash
    * 貢獻者: https://github.com/ccckmit/ccclodash
3. 貢獻者分支專案，例如叫 develop1，然後發一個 pull request 給主導者，說要新增一個稱為 xxx 的函數
    * 主導者在 pull request 上回應是否允許，或者給許意見想法！
4. 貢獻者新增完成 xxx 的函數與測試，並且 push 回自己的專案，然後再發送 pull request 給主導者，請求合併
    * 
5. 主導者透過下列指令下載貢獻者的提交版本
    * git remote add 來源名稱(例如 ccckmit) 來源專案網址(例如 https://github.com/ccckmit/ccclodash)
    * git fetch 來源名稱(例如 ccckmit)
6. 主導者用 marge 合併該版本並測試是否正常
    * git checkout -b 測試分支名稱(例如 ccckmit-develop1)     // 這個動作會從 master 分支出 ccckmit-develop1
    * git merge -b ccckmit/develop1
    * 執行 mocha 指令測試
7. 測試沒問題後，有兩個方法接受 pull request ，請擇一使用
    * a. 使用 git checkout master; git merge ccckmit/develop1; git push origin master 將合併後的版本推回
    * b. 回到主導者 github 專案，去接收 pull request 核可之。(這時貢獻者的版本就合併進來了)

### 練習 3 -- 雙人合作 (Master/Slave 的方式)

請重複上一個練習，但這次不再一人扮演兩角，而是採用兩個人合作的方式。

1. 兩個人一組，其中一個扮演 master，另一個扮演 slave。
2. Slave 先 fork master 的先前專案。
3. Slave clone 該 fork 版本，將自己的函數加入到專案當中
4. Slave 測試沒問題後，將專案 push 回自己 fork 的版本中。
5. Slave 發送 pull request 請求給 master ，請 master 收取新功能。
6. Master 接收並測試，確認沒問題後接受 pull request.



學完這章您應該已經具備《使用GIT 合作的能力》，下一章的重點將會是《提高程式品質，除錯與避免錯誤的能力》的能力！

