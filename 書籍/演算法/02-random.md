## 亂數產生法 Random

### 亂數產生

方法 1 : https://github.com/cccbook/algjs/blob/master/code/06-random/random.js

```js
var seed = 371
const SEED_MAX = 9999997

function random() {
    seed = (seed+37 ) % SEED_MAX
    var x = Math.sin(seed) * 93177
    return x - Math.floor(x);
}

module.exports = random
```

方法 2 : https://github.com/cccbook/algjs/blob/master/code/06-random/random2.js

```js
// 來源：https://stackoverflow.com/questions/521295/seeding-the-random-number-generator-in-javascript
var m_w = 123456789;
var m_z = 987654321;
var mask = 0xffffffff;

// Takes any integer
function seed(i) {
    m_w = i;
    m_z = 987654321;
}

// Returns number between 0 (inclusive) and 1.0 (exclusive),
// just like Math.random().
function random()
{
    m_z = (36969 * (m_z & 65535) + (m_z >> 16)) & mask;
    m_w = (18000 * (m_w & 65535) + (m_w >> 16)) & mask;
    var result = ((m_z << 16) + m_w) & mask;
    result /= 4294967296;
    return result + 0.5;
}

module.exports = { random, seed }
```

方法 3 : https://github.com/cccbook/algjs/blob/master/code/06-random/random3.js

```js
const M = {}

M.seed = function(s) {
  return function() {
      s = Math.sin(s) * 10000;
      return s - Math.floor(s);
  };
};

// usage:
var random1 = M.seed(42);
var random2 = M.seed(random1());
M.random = M.seed(random2());

module.exports = M

```

### 非均等分佈之亂數產生 -- 逆變換法


* https://github.com/cccbook/algjs/blob/master/code/06-random/distribution/rexp.js

```js
/*

定理： 對任一連續分佈 F, 隨機變量 $X = F^{-1}(U)$ 的分佈為 F

參考： https://zh.wikipedia.org/wiki/%E9%80%86%E5%8F%98%E6%8D%A2%E9%87%87%E6%A0%B7

範例： 指數分佈的密度函數為 $f(x) = \lambda e^{-lambda x}$ 

其累積密度函數為 ＄F(x) = 1-e^{-\lambda} x$ ， 

Ｆ的逆變換為 $invF = -1/{\lambda} log(1-U)$

因此我們可以用 invF 來產生該分佈的樣本。

*/

function rexp(lambda) {
  return (-1/lambda) * Math.log(1-Math.random())
}

for (let i=0; i<100; i++) {
  console.log('rexp(20)=', rexp(20))
}
```

執行結果：

```
csienqu-teacher:distribution csienqu$ node rexp
rexp(20)= 0.06376054891755753
rexp(20)= 0.021547350775182456
rexp(20)= 0.003924013147755614
rexp(20)= 0.06442474032283624
rexp(20)= 0.04075782008572337
rexp(20)= 0.07957684006591255
rexp(20)= 0.004048475667393208
rexp(20)= 0.0725709113584828
...
rexp(20)= 0.0036578005705508857
rexp(20)= 0.007995594176028487
rexp(20)= 0.0341919271281008
rexp(20)= 0.0041195594418374495
rexp(20)= 0.022637911380867494
```

### UUID 的產生

```js
// https://stackoverflow.com/questions/105034/create-guid-uuid-in-javascript

function uuidv4() {
  return 'xxxxxxxx-xxxx-4xxx-yxxx-xxxxxxxxxxxx'.replace(/[xy]/g, function(c) {
    var r = Math.random() * 16 | 0, v = c == 'x' ? r : (r & 0x3 | 0x8)
    return v.toString(16)
  })
}

console.log(uuidv4())
```

執行結果

```
csienqu-teacher:06-random csienqu$ node uuid
15f9d0e3-fca1-42ea-8657-51d7ee2d19ce
csienqu-teacher:06-random csienqu$ node uuid
9f5e13ca-9fa5-415a-bd19-5da039efdb58
csienqu-teacher:06-random csienqu$ node uuid
c1e2f29e-fb11-462d-94b0-5bff2fa072e1
csienqu-teacher:06-random csienqu$ node uuid
a1cf99c2-2a73-4a55-b33c-1e389a105ffb
```
