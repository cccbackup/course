## 查表法 Table Lookup

### 翻譯系統 (簡易英翻中)

執行結果

```
$ node e2c a dog chase a cat
[ '一隻', '狗', '追', '一隻', '貓' ]
```

程式碼

```javascript
var e2c = { dog:"狗", cat:"貓", a: "一隻", chase:"追", eat:"吃" };

function mt(e) {
  var c = [];
  for (i in e) {
    var eword = e[i];
    var cword = e2c[eword];
    c.push(cword);
  }
  return c;
}

var c = mt(process.argv.slice(2));
console.log(c);
```

執行結果：

```
$ node e2c.js a dog
[ '一隻', '狗' ]
$ node e2c.js a dog chase a cat
[ '一隻', '狗', '追', '一隻', '貓' ]
$ node e2c.js a dog chase a car
[ '一隻', '狗', '追', '一隻', undefined ]
```

補充說明：請注意上面的 e2c[eword] 這一行不能改用 e2c.eword, 原因是 e2c.eword 是在查詢 eword 這個詞，也就是 e2c['eword'] 的意思，上面範例中e2c['eword']  會是 undefined。

e2c[eword] 才是在查詢像 e2c['dog'] 這樣的內容。

請看下列的示範：

```
> var e2c = { dog:"狗", cat:"貓", a: "一隻", chase:"追", eat:"吃" };
undefined
> e2c
{ dog: '狗', cat: '貓', a: '一隻', chase: '追', eat: '吃' }
> e2c.eword
undefined
> var eword='dog'
undefined
> eword
'dog'
> e2c.eword
undefined
> e2c['dog']
'狗'
> e2c[eword]
'狗'
```


### 用查表加速 -- 以費氏數列為例

傳統用遞迴方式的費氏數列算法，會耗費很久的時間：

```js
function fibonacci (n) {
  if (n < 0) throw Error('fibonacci:n < 0')
  if (n === 0) return 0
  if (n === 1) return 1
  return fibonacci(n - 1) + fibonacci(n - 2)
}

var startTime = Date.now()
console.log('fibonacci(43)=', fibonacci(43))
var endTime = Date.now()
var milliSeconds = endTime - startTime
console.log('time:%dms', milliSeconds)

```

執行結果:

```
$ node .\fiboanacci.js
fibonacci(43)= 433494437
time:25530ms
```

加入查表，讓已經算過的就不需要算第二次，第二次之後改用查的！

```js
var fib = [0, 1]

function fibonacci (n) {
  if (n < 0) throw Error('fibonacci:n < 0')
  if (fib[n] != null) return fib[n]
  fib[n] = fibonacci(n - 1) + fibonacci(n - 2)
  return fib[n]
}

var startTime = Date.now()
console.log('fibonacci(43)=', fibonacci(43))
var endTime = Date.now()
var milliSeconds = endTime - startTime
console.log('time:%dms', milliSeconds)

```

執行結果

```
$ node .\fiboanacci_lookup.js
fibonacci(43)= 433494437
time:14ms
```

### 用查表加速 C(n,k) 函數

排列組合中的 C(n, k) 函數，其定義為 n!/(k!(n-k!)) ，我們可以直接套公式計算之。

```js
function factorial(n) {
  var p = 1
  for (i=1; i<=n; i++) {
    p = p * i;
  }
  return p
}

function c(n, k) {
  return factorial(n) / (factorial(k)*factorial(n-k))
}

console.log("c(5,2)=", c(5,2))
console.log("c(7,3)=", c(7,3))
console.log("c(12,5)=", c(12,5))
console.log("c(60,30)=", c(60,30))
```

執行結果如下：

```
$ node .\Cnk
c(5,2)= 10
c(7,3)= 35
c(12,5)= 792
c(60,30)= 118264581564861470
```

其中前三個答案是對的，但是第四個 c(60, 30) 的答案很接近，但卻是錯的，因為計算過程中的 `factorial(60) = 60!` 太大，導致javascript 的雙精度浮點數無法精確表示，於是原本應該 c(60, 30) = 118264581564861420 ，卻計算出了 c(60, 30) = 118264581564861470 了！

對於 c(n,k) 函數，我們還可以採用《帕斯卡公式》(Pascal's rule) 進行遞迴計算，其算式如下：

C(n,k) = C(n-1, k-1) + C(n-1,k)     for (1 <=k<=n)

於是我們可以寫出下列遞迴式：

```js
function c(n, k) {
  if (k < 0 || k > n) return 0
  if (k > n-k) k = n - k
  if (k==0 || n <= 1) return 1
  return c(n-1, k) + c(n-1, k-1)
}

console.log("c(5,2)=", c(5,2))
console.log("c(7,3)=", c(7,3))
console.log("c(12,5)=", c(12,5))
console.log("c(60,30)=", c(60,30))
```

但是這個遞迴重複計算了太多次，導致執行 c(60, 30) 時會很久出不來，感覺好像當掉了，以下是執行結果 ...

```
PS D:\ccc\book\algjs\code\09-dynamicProgramming\combinatorial> node .\CnkR
c(5,2)= 10
c(7,3)= 35
c(12,5)= 792   // 後面就很久出不來了 ....
```

如果我們採用《查表法》的方式加速遞迴式，那麼很快就能計算出來了，以下是加了查表法的遞迴程式

```js
var C = []

function c(n, k) {
  if (k < 0 || k > n) return 0
  if (k > n-k) k = n - k
  if (C[n] == null) C[n] = []
  if (C[n][k] != null) return C[n][k]
  if (k==0 || n <= 1)
    C[n][k] = 1
  else 
    C[n][k] = c(n-1,k) + c(n-1, k-1)
  return C[n][k]
}

console.log("c(5,2)=", c(5,2))
console.log("C=%j", C);
console.log("c(7,3)=", c(7,3))
console.log("c(12,5)=", c(12,5))
console.log("c(60,30)=", c(60,30))
```

執行結果:

```
PS D:\ccc\book\algjs\code\09-dynamicProgramming\combinatorial> node .\CnkRLookup
c(5,2)= 10
C=[null,[1],[1,2],[1,3],[null,4,6],[null,null,10]]
c(7,3)= 35
c(12,5)= 792
c(60,30)= 118264581564861420
```

### 結語

對於需要重複計算的事項，我們只要先記在表格裡面，下次需要時就不需要再次計算，只要從表格裡面查出來就行了！

如果該計算比查表時間多，那麼這樣的方法就可以加快速度！




