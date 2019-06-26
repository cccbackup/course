# 密碼學算法 Cryptography

## 對稱性加解密

對稱性加解密的方法有很多，像是DES、3DES、AES、Blowfish、IDEA、RC5、RC6 等等。

所謂的『對稱性』是指加解密所用的金鑰 key 是相同的，因此只要雙方都擁有該組金鑰，就可以成功的完成『加密後解密』的動作。

在此我們以 node.js 的 crypto 模組來展示 AES 加解密算法的過程。

檔案： aes.js

```js
var crypto = require('crypto')
var algorithm = 'aes-256-ctr'
var password = 'd6F3Efeq'

function encrypt(text) {
  var cipher = crypto.createCipher(algorithm, password)
  var crypted = cipher.update(text,'utf8','hex')
  crypted += cipher.final('hex');
  return crypted;
}
 
function decrypt(text) {
  var decipher = crypto.createDecipher(algorithm, password)
  var dec = decipher.update(text,'hex','utf8')
  dec += decipher.final('utf8');
  return dec;
}
 
var plainText  = "hello world"
var cipherText = encrypt(plainText)
var decryptText = decrypt(cipherText)
console.log('plainText  =', plainText)
console.log('cipherText =', cipherText)
console.log('decryptText=', decryptText)
``` 

執行結果：

```
$ node aes
plainText  = hello world
cipherText = 0c8bd89c2e316f7f2245e0
decryptText= hello world
```

## 非對稱性加解密

簡易 RSA 實作 (不支援超長整數）

檔案： simpleRsa.js

```js
unction mpower(a, n, p) {
  let r = a
  for (let i=2; i<=n; i++) {
    r = (r * a) % p
  }
  return r
}

var p = 61, q = 53, N = p*q // lcm(61,53)=780
let e = 17 , d = 413

// var p = 37, q = 67, N = p * q
// let e = 23, d = 

var M1 = [65, 22, 37, 18, 29]
var E1 = []
var M2 = []
for (let m of M1) {
  let c = mpower(m, e, N)
  E1.push(c)
  let m2 = mpower(c, d, N)
  M2.push(m2)
}

console.log('M1=', M1)
console.log('E1=', E1)
console.log('M2=', M2)
```

執行結果

```
$ node simpleRsa.js
M1= [ 65, 22, 37, 18, 29 ]
E1= [ 2790, 2558, 1350, 2100, 1912 ]
M2= [ 65, 22, 37, 18, 29 ]
```

## 電子簽章與驗證

```js
// openssl genrsa  -out server.pem 1024
// openssl req -key server.pem -new -x509 -out cert.pem

var crypto = require('crypto')
var fs = require('fs')

function signer(algorithm, privateKey, data){
  var signer = crypto.createSign(algorithm);
  signer.update(data);
  sigature = signer.sign(privateKey, 'hex');
  return sigature
}

function verify(algorithm, publicKey, sigature, data){
  var verify = crypto.createVerify(algorithm);
  verify.update(data);
  return verify.verify(publicKey, sigature, 'hex')
}

var algorithm = 'RSA-SHA256'
var data = "The data to be signed!"
var privateKey = fs.readFileSync('server.pem').toString()
var signature = signer(algorithm, privateKey, data)

var publicKey = fs.readFileSync('cert.pem').toString()
console.log('verify(data)=', verify(algorithm, publicKey, sigature, data))         // 驗證是否為公鑰發出者 (私鑰擁有者)
console.log('verify(data+xxx)=', verify(algorithm, publicKey, sigature, data + "xxx"))

```

產生證書

```
$ openssl genrsa  -out server.pem 1024
Generating RSA private key, 1024 bit long modulus
..+++++
...+++++
e is 65537 (0x10001)
csienqu-teacher:sign csienqu$ openssl req -key server.pem -new -x509 -out cert.pem
You are about to be asked to enter information that will be incorporated
into your certificate request.
What you are about to enter is what is called a Distinguished Name or a DN.
There are quite a few fields but you can leave some blank
For some fields there will be a default value,
If you enter '.', the field will be left blank.
-----
Country Name (2 letter code) [AU]:TW
State or Province Name (full name) [Some-State]:Kinmen
Locality Name (eg, city) []:Kinmen
Organization Name (eg, company) [Internet Widgits Pty Ltd]:nqu
Organizational Unit Name (eg, section) []:csie
Common Name (e.g. server FQDN or YOUR name) []:ccckmit
Email Address []:ccckmit@gmail.com
```

執行結果

```
$ node sign
verify(data)= true
verify(data+xxx)= false
```


## 參考

* [Node.js加密算法库Crypto](http://blog.fens.me/nodejs-crypto/)
* [AES-JS：JavaScript 的AES 對稱式資料加密工具- G. T. Wang](https://blog.gtwang.org/programming/javascript-aes-symmetric-encryption-tutorial/)
* 進階: 量子電腦 -- [Quantum Computing Concepts](https://www.youtube.com/playlist?list=PL50XnIfJxPDWDyea8EbbLe8GHfXkWU7W_)