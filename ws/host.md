# 用 node.js 架站 -- 上線營運

## 完整專案 -- mdbook

專案開發通常是一個漫長的過程，並不像那些範例一樣，感覺好像一下就完成了。

## Bookdown 書籍出版平台

為了讓大家體會專案開發的過程，我把自己開發 Bookdown 這個書籍出版網站的歷程記錄在下列 github 專案中，成為一系列的《開發紀錄》，您可以透過這個專案，逐步體會我在開發這個專案時的經過。

* <https://github.com/ccckmit/road_to_bookdown>

後來我把這個專案放到 github 上開放原始碼，並且登錄到 npm 上，成為 mdbook 專案！

* <https://github.com/ccckmit/mdbook>
* <https://www.npmjs.com/package/mdbook>

建議您先將 mdbook 安裝起來，並且啟用使用，試試這個 Markdown 電子書編輯出版平台。

理解運作方式後，請仔細閱讀上述程式碼，以瞭解一個專案是如何從零開始建構起來的。

有了這樣的專案之後，您就可以準備上線了！

## 上線到 mdbookspace.com

開發完 Bookdown 之後，我把該網站上線了，原本只是在學校的伺服器上給自己用而已，但是在 2017 年農曆新年，學校更換設備之後，導致我的伺服器無法連上，後來我決定乾脆上線到《雲端虛擬主機》，於是就買了每個月 $5 美金的 Digital Ocean 虛擬主機帳號，並買了 mdbookspace.com 這個網址。

因此您可以在下列網址上看到 Bookdown 系統現在的狀況。

* <https://mdbookspace.com>

在上線完成之後，我寫了一篇 [《用十分鐘將你的網站送上雲端》](https://www.slideshare.net/ccckmit/ss-72398210) 的《十分鐘系列》投影片描述整個過程，您可以跟著這份文件試試看將自己的網站上線。

當您學會用 Node.js 寫網站之後，最好上線去試試身手，還有甚麼比創造一個網站上線營運更能讓您完整體會學會 Node.js 之後的成就感呢？

現在、該你來開發自己的專案，並且將該專案上線了！

## 十分鐘投影片

1. [十分鐘讓程式人搞懂雲端平台與技術](http://www.slideshare.net/ccckmit/ss-70782470)
2. [用十分鐘將你的網站送上雲端](https://www.slideshare.net/ccckmit/ss-72398210)

## 上線步驟：
1. 到 DigitalOcean 申請一個站 (DigitalOcean 稱一個站為 Droplet，我使用 $5 美元的 ubuntu linux 虛擬主機方案)。
    * 用 putty 連上去 server 之後，安裝相關軟體
    * 在 server 安裝 sftpd 以便將檔案上傳
    * 若你用 windows, 在 Client 裝 WinSCP 以便連上 server 並上傳檔案。(用 git/github/gitbucket 也行)
    * 將專案上傳後，啟動 server 程式 (最好採用 pm2 之類的方式啟動網站，這樣才不會在 logout 或退出 putty 的時候導致 server 被關掉)
    * 直接打 ip (我的站為  http://139.59.108.105 ) 測試看看網站是否正常運作。
    * 開通帳號時可以設 SSH 或只用密碼，我有用 SSH。
    * 請參考： [How To Use SSH Keys with PuTTY on DigitalOcean Droplets -- Windows users](https://www.digitalocean.com/community/tutorials/how-to-use-ssh-keys-with-putty-on- digitalocean-droplets-windows-users) 
2. 到 GoDaddy 或 freenom 等網站上購買網域名稱。
    * 申請網域名稱，然後上去設定 domain=>ip 的對應關係 (我的網域 mdbookspace.com 是向 GoDaddy 申請的，第一年很便宜，只要台幣 45 元，但第二年以後就會變貴，好像要五百多元)
3. 取得 LetsEncrypt 的 SSL 證書
    * 如果有需要 https (ssl) ，那麼最好申請合格證書 (自簽證證書會導致瀏覽器有警告的叉叉，要申請免費的合格證書現在最好的方式是用 LetsEncrypt。由於 LetsEncrypt 標準程序主要支援 Nginx/Apache，所以經由網友建議後，我採用 Nginx 反向代理，然後將 80 轉到 443，並由 443 完成認證加密程序後，轉到我自己的 8080 port 去，這樣 node.js 裡也就不需要支援 SSL 就可以得到安全保護了)。
    * DigitalOcean 上的資料寫得很完整，有興趣的人可以參考下列文件！
    * [How To Set Up a Node.js Application for Production on Ubuntu 16.04](https://www.digitalocean.com/community/tutorials/how-to-set-up-a-node-js-application-for-production-on-ubuntu-16-04)
    * [How To Secure Nginx with Let's Encrypt on Ubuntu 14.04](https://www.digitalocean.com/community/tutorials/how-to-secure-nginx-with-let-s-encrypt-on-ubuntu-14-04)
    * 最後用自動排程更新證書 sudo crontab -e (因為 LetsEncrypt 的證書每三個月都要更新一次)

更新證書的手動作法

```
$  sudo systemctl stop nginx // nginx -s stop
$  sudo certbot renew
$  nginx
$  pm2 start bookServer
```

Nginx 設定檔位於

```
root@ubuntu-512mb-sgp1-01:~# nginx -t
nginx: the configuration file /etc/nginx/nginx.conf syntax is ok
nginx: configuration file /etc/nginx/nginx.conf test is successful
```

但我的 nginx 設定檔位於

```
/etc/nginx/sites-enabled/default
```




## 上線需要注意的調整

* [Express 正式作業最佳作法：效能和可靠性](http://expressjs.com/zh-tw/advanced/best-practice-performance.html)

## 網站維護

網站設計完上線之後，通常不是就這樣一直運行下去，設計者會根據人們的使用情況，來決定進行那些功能調整，或者是修改程式。

從我設計 bookdown 在學校上線，直到放上 mdbookspace.com ，也經過了快一年了，有時我還會發現一些功能、流程或程式上的問題，於是會進行修正。

自己設計網站的好處是，可以持續修正到您滿意為止，並且可以不斷開發讓系統更加完善，讓使用更加順暢。

當然、這也得花費一些時間，不過對於一個 Node.js 的程式設計者而言，我想是非常值得的，因為我們會從中學到許多《寫程式與經營網站》的知識，讓自己成為一個真正的 Node.js 程式人與網站經營者。

現在、該你來經營自己的網站了！

## 維護技巧

1 - 使用 pm2 啟動伺服器

* <http://pm2.keymetrics.io/>

2 - 更新 node.js

* <http://askubuntu.com/questions/426750/how-can-i-update-my-nodejs-to-the-latest-version>

```
Use n module from npm in order to upgrade node

sudo npm cache clean -f
sudo npm install -g n
sudo n stable

sudo ln -sf /usr/local/n/versions/node/<VERSION>/bin/node /usr/bin/node 
To upgrade to latest version (and not current stable) version, you can use

sudo n latest
```

3 - 在 mac 上

安裝 putty 並登入

```
  506  ssh -i privateKey.ppk root@mdbookspace.com
  507  brew install putty
  508  puttygen privatekey.ppk -O private-openssh -o privatekey.pem
  509  ssh -i privatekey.pem root@mdbookspace.com
  510  chmod go-rw privatekey.pem
  511  ssh -i privatekey.pem root@mdbookspace.com
```

ftp 檔案上傳下載

* [Unix / Mac / Linux 下直接用scp傳送檔案](http://blog.riaproject.com/server-setting/1644/unix-mac-linux-%E4%B8%8B%E7%9B%B4%E6%8E%A5%E7%94%A8scp%E5%82%B3%E9%80%81%E6%AA%94%E6%A1%88.html)

## 多台伺服器流量平衡

* [使用 HAProxy 完成 網站分流, 平衡負載](https://blog.longwin.com.tw/2009/03/haproxy-ha-load-balance-2009/)

* [富人用 L4 Switch，窮人用 Linux HAProxy！](https://blog.toright.com/posts/3967/%E5%AF%8C%E4%BA%BA%E7%94%A8-l4-switch%EF%BC%8C%E7%AA%AE%E4%BA%BA%E7%94%A8-linux-haproxy%EF%BC%81.html)

## 更新所有 package.json 中的 npm 套件

```
$ npm install -g npm-check-updates
$ npm-check-updates -u
$ npm install 
```

## 更新重啟動

```
$ sudo apt-get update
$ sudo apt-get dist-upgrade
$ sudo shutdown -r now
```

