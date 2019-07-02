# git / github 的用法

## github

* 到 https://github.com/cccnqu/ 選擇你上的課程，並進行 fork 動作
* 到 wiki 區開始寫你的課程筆記，該筆記格式採用 [Markdown](Markdown) 語法
* 看看該課程專案的結構，包含程式與 wiki 教材等等。

## 安裝

* 到 https://git-scm.com/downloads 下載 git 軟體並安裝
* 打入 git 指令，應該會出現下列訊息

```
$ git
usage: git [--version] [--help] [-C <path>] [-c name=value]
           [--exec-path[=<path>]] [--html-path] [--man-path] [--info-path]
           [-p | --paginate | --no-pager] [--no-replace-objects] [--bare]
           [--git-dir=<path>] [--work-tree=<path>] [--namespace=<name>]
           <command> [<args>]

...
``` 

## 最常用的 git 指令

```
$ git clone https://github.com/xxxxxxx/wd106b.git
... 若你是修改後還要推回的，xxxxxxx 應該是你自己的帳號 ...
... 若只是要 clone 老師的，那 xxxxxx 應該是 cccnqu ...

$ cd wd106b  註: 切換到 clone 的資料夾 wd106b 當中

... 接著加入一些新檔案，或者修改某些檔案後 ...

$ git add -A
$ git commit -m "xxxxxxxx"
$ git push origin master
Username : xxxxxx    <-- 輸入你的帳號 (github 上的)
Password :           <-- 輸入你的密碼
注意：在 Password 裡你打任何字，都不會印出來 (也不會印 * 號)，這是正常的。 (不要覺得為何打了沒反應 ....)
...
```

如果你是第一次在自己電腦上用 git push，那麼必須要先設定自己的 email 和 name， name 必須是 github 上的帳號。

```
$ git config --global user.email "xxxxx@gmail.com"
$ git config --global user.name "xxxxx"
```

## git push 失敗時的處理

在 Mac 上若沒問密碼且推不上去，很可能是裡面已經有設 ssh 證書，請用下列指令清掉。

```
$ git credential-osxkeychain erase
host=github.com
protocol=https
<press return>
```

如果 github 上的版本比你 local 的新，那麼可能會有訊息提示，此時可以用 pull 把遠端新的資料拉下來，指令如下：

```
$ git pull origin master
```

在 WINDOWS 底下，可以用 控制台\所有控制台項目\認證管理員\WINDOWS 認證 去刪除 GITHUB 的證書，然後再重新 push 就行了!

## 架網站

若要用 github 架網站，上傳後把 github 網頁的網址貼到 rawgit 上

* https://rawgit.com/

得到的網址就是公開網頁的網址，用瀏覽器看就行了！

## 與老師的專案同步

* https://gist.github.com/CristinaSolana/1885435

```
$ git remote add upstream git://github.com/cccnqu/wd106b.git
$ git fetch upstream
$ git pull upstream master
```

再推回你自己的 github 中

```
$ git push origin master
```

## 用 github 架站 -- github pages

最新作法請參考 -- https://pages.github.com/

以下是舊的做法，應該還是可以用：

到你 github 專案的 setting (例如 https://github.com/ccckmit/wd107b/settings ) 裏，找到 GitHub Pages 那一段，在 source 點選成 master branch ，然後該頁會從新整理後，出現一個像 https://ccckmit.github.io/wd107b/ 這樣的網址，這樣你的網站就公開在網路上了。

接著將路徑（例如exercise/ccc.html）補在公開站後面，變成 https://ccckmit.github.io/wd107b/exercise/ccc.html ，這樣就可以看到網頁了！

## 圖形介面

* [GitKraken – 好用的垮平台Git GUI](https://wordpress.lokidea.com/blog/1624/gitkraken-%E5%A5%BD%E7%94%A8%E7%9A%84%E5%9E%AE%E5%B9%B3%E5%8F%B0git-gui/)

## 更深入的 git 教學資源

* [Pro Git book 簡體中文版](https://git-scm.com/book/zh/v2)
* [Yodalee 的 Git 教學影片系列](http://yodalee.blogspot.tw/2017/12/git-video.html?m=1)
* [陳鍾誠的軟體工程課 -- Git 指南](https://github.com/cccnqu/se106a/wiki/git.md)
* [陳鍾誠的軟體工程課 -- Github 指南](https://github.com/cccnqu/se106a/wiki/github.md)
* [利用 Github Classroom 加 Travis CI 打造改作業系統](https://blog.techbridge.cc/2018/02/03/github-classroom-and-travis-ci/)

