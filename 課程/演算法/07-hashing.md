## 雜湊法 Hashing 

### 簡易雜湊函數

* https://github.com/cccbook/algjs/blob/master/code/11-hashing/hash.js

```js
function hash(str) {
  let hash = 5381
  let i = str.length

  while(i) {
    hash = (hash * 33) ^ str.charCodeAt(--i);
  }

  /* JavaScript does bitwise operations (like XOR, above) on 32-bit signed
   * integers. Since we want the results to be always positive, convert the
   * signed int to an unsigned by doing an unsigned bitshift. */
  return hash >>> 0;
}


console.log('hash(hello)=', hash('hello').toString(16))
console.log('hash(hello!)=', hash('hello!').toString(16))
```

執行結果

```
$ node hash
hash(hello)= acfa3a7
hash(hello!)= c21a8b86
```

### SHA256 雜湊函數

SHA256 是 Secure Hash Algorithm 2 的成員， Node.js 內建函式庫的密碼學套件 crypto 支援了很多這類算法。

範例: https://github.com/cccbook/algjs/blob/master/code/11-hashing/digest.js

```js
const crypto = require('crypto');

const secret = 'abcdefg';
const hash = crypto.createHmac('sha256', secret)
                   .update('I love cupcakes')
                   .digest('hex')
console.log(hash)
```

執行結果

```
$ node digest
c0fa1bc00531bd78ef38c628449c5102aeabd49b5dc3a2a516ea6ea959d6658e
$ node digest
c0fa1bc00531bd78ef38c628449c5102aeabd49b5dc3a2a516ea6ea959d6658e
$ node digest
c0fa1bc00531bd78ef38c628449c5102aeabd49b5dc3a2a516ea6ea959d6658e
```

### Git 版本管理

* https://github.com/anders94/blockchain-demo/commits/master

其中一版

* https://github.com/anders94/blockchain-demo/commit/6c870c33bb361f76e64baf1dd5aea06ebab1762c

### Bitcoin 比特幣

* https://anders.com/blockchain/
    * https://github.com/anders94/blockchain-demo

### Libra 天秤幣

* [全球央行紅色警戒，臉書幣Libra為何可能超越比特幣](https://www.cw.com.tw/article/article.action?id=5095751)

### 習題

1. 請問以下的項目是『雜湊』還是『亂數』
    * MongoDB 的 ObjectId -- https://docs.mongodb.com/manual/reference/method/ObjectId/
    * Github 的 repository id -- https://github.com/cccbook/algjs/commit/2ca32deea6b1270c713cda9e5f6498a963aaa104
    * 微軟提出的 UUID -- https://zh.wikipedia.org/wiki/%E9%80%9A%E7%94%A8%E5%94%AF%E4%B8%80%E8%AF%86%E5%88%AB%E7%A0%81
    * 比特幣裡面那串 16 進位碼 -- https://www.blockchain.com/zh/btc/block/000000000000000000135eaa3ede9deb121d536f056a9dbd8d094e09bf1e0d4a


