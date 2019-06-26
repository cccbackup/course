# 動態規劃法 Dynamic Programming

動態規劃是透過表格的方式，逐步由前面的結果推算出後面結果的方法。

在《查表法》的主題中，我們介紹了 [如何用《查表法》計算 C(n,k) 函數](https://github.com/cccbook/algjs/wiki/01-tableLookup) ，在此我們將改用《動態規劃》的方式重新設計 C(n,k) 函數！

假如不用查表法，我們也可以用《逐步建表法》，用類似遞迴的公式，由 c[n-1][k-1] + c[n-1][k] => c[n][k] 從小到大逐步計算每個表格中元素的值！

這種逐步建表法，其實就是一種動態規劃法。

以下是 c(n,k) 問題的動態規劃程式：

```js
// http://mathworld.wolfram.com/PascalsFormula.html
// https://en.wikipedia.org/wiki/Pascal%27s_rule
// https://en.wikipedia.org/wiki/Pascal%27s_triangle
// https://en.wikipedia.org/wiki/Binomial_coefficient
/*
c(n, k) = 0                        , if n < k
        = 1                        , if k = 0 or k = n
        = c(n-1, k-1) + c(n-1, k)  , if k <= n-k
        = c(n, n-k)                , if k > n-k
*/

function c(N, K) {
  var C = [];
  for (let n=0; n<=N; n++) {
    C[n] = [1]
    C[0][n] = 0
  }
  for (let n=1; n<=N; n++) {
    for (let k=1; k<=N; k++) {
      let k0 = (k <= n-k) ? k : n-k
      if (n < k)
        C[n][k] = 0
      else if (n===k)
        C[n][k] = 1
      else
        C[n][k] = C[n][n-k] = C[n-1][k0-1] + C[n-1][k0]
    }
  }
  /*
  for(let n=0; n<=N; n++) {
    console.log("C[%d]=%j", n, C[n])
  }
  */
  return C[N][K];
}

console.log("c(5,2)=", c(5,2))
console.log("c(7,3)=", c(7,3))
console.log("c(12,5)=", c(12,5))
console.log("c(60,30)=", c(60,30))
```

## 字串編輯距離

Vladimir Levenshtein 在 1965 年提出了《字串編輯距離》的問題並給了一個演算法進行計算，因此 《字串編輯距離》被稱為 Levenshtein distance。

關於字串編輯距離的詳細描述請參考 [Wikipedia: Levenshtein distance](https://en.wikipedia.org/wiki/Levenshtein_distance) ，以下是實作程式。

檔案： editDistance.js

```js
function editDistance (a, b){
  if(a.length == 0) return b.length; 
  if(b.length == 0) return a.length; 

  var m = [];
  for (let i = 0; i <= b.length; i++) m[i] = [i]
  for(let j = 0; j <= a.length; j++) m[0][j] = j

  for(i = 1; i <= b.length; i++){
    for(j = 1; j <= a.length; j++){
      if(b.charAt(i-1) == a.charAt(j-1)){
        m[i][j] = m[i-1][j-1]
      } else {
        m[i][j] = Math.min(m[i-1][j-1] + 1, // 取代
                           Math.min(m[i][j-1] + 1, // 插入
                                    m[i-1][j] + 1)); // 刪除
      }
    }
  }

  return m[b.length][a.length];
}

var a, b

a = "010100001"
b = "010100010"
console.log("dist(%s,%s) = %s", a, b, editDistance(a,b))

a = "ATGCAATCCC"
b = "ATGATCCG"
console.log("dist(%s,%s) = %s", a, b, editDistance(a,b))
```

執行結果:

```
$ node .\editDistance.js
dist(010100001,010100010) = 2
dist(ATGCAATCCC,ATGATCCG) = 3
```

隨堂練習：請印出兩個字串最小編輯距離的對齊方式。

範例： 
```
$ node .\editDistance.js
dist(ATGCAATCCC,ATGATCCG) = 3
align(ATGCAATCCC,ATGATCCG)
b = ATG A TCCG
a = ATGCAATCCC 
```

範例：

## 維特比演算法 (Viterbi Algorithm)

維特比演算法是高通創辦人 Viterbi 所設計的一個方法，原本是用來去除通訊系統雜訊用的，後來在《語音辨識與自然語言處理領域》也很常被使用，因為維特比演算法可以很快地計算《隱馬可夫模型》的最可能隱序列。

關於《隱馬可夫模型》與《維特比演算法》的說明，請參考下列文章：

* [維基百科:維特比演算法](https://zh.wikipedia.org/wiki/%E7%BB%B4%E7%89%B9%E6%AF%94%E7%AE%97%E6%B3%95)

《維特比演算法》是用來尋找產生某『表現序列』的最可能『隱狀態序列』，以下是我們用程式 Viterbi.js 計算的結果：

範例：根據下列規則，請問『喵 喵 汪』中每個詞彙最可能的詞性會是什麼？

轉移機率與規則

```
N 0.6 => 喵 0.4 | 汪 0.6
V 0.4 => 喵 0.5 | 汪 0.5

    N   V
 N  0.3 0.7
 V  0.8 0.2
```

執行結果

```
$ node viterbi
t=1 path={"N":["V","N"],"V":["N","V"]}
t=2 path={"N":["N","V","N"],"V":["V","N","V"]}
T=[{"N":0.24,"V":0.2},{"N":0.06400000000000002,"V":0.08399999999999999},{"N":0.040319999999999995,"V":0.022400000000000003}]
prob=0.040319999999999995 path=["N","V","N"]
```

以下是該程式的原始碼：

```js
// 參考： https://zh.wikipedia.org/wiki/%E7%BB%B4%E7%89%B9%E6%AF%94%E7%AE%97%E6%B3%95

// N 0.6 => 喵 0.4 | 汪 0.6
// V 0.4 => 喵 0.5 | 汪 0.5
//    N   V
// N  0.3 0.7
// V  0.8 0.2
const P = {
  'N': 0.6,
  'V': 0.4,
  'N=>N': 0.3,
  'N=>V': 0.7,
  'V=>N': 0.8,
  'V=>V': 0.2,
  'N=>喵': 0.4,
  'N=>汪': 0.6,
  'V=>喵': 0.5,
  'V=>汪': 0.5,
}

function argmax(list) {
  let max = Number.NEGATIVE_INFINITY, index = null
  for (let k in list) {
    if (list[k] > max) { index=k; max=list[k] }
  }
  return {max, index}
}

function viterbi(obs, states, P) {
  console.log('觀察到的序列=', obs)
  const T = [{}] // Viterbi Table
  let path = {}  // path[state] = 從 0 到 t 到達 state 機率最大的 path
  for (let y of states) { // # Initialize base cases (t == 0)
    T[0][y] = P[y] * P[y+'=>'+obs[0]]
    path[y] = [y]
  }
  // console.log('T=%j path=%j', T, path)
  for (let t=1; t<obs.length; t++) { // # Run Viterbi for t > 0
    T[t] = {}
    let newpath = {}
    for (let y of states) {
      let {max:prob, index:si} = argmax(states.map((y0)=>T[t-1][y0] * P[y0+'=>'+y] * P[y+'=>'+obs[t]]))
      let state = states[si]
      // console.log('y=%s prob=%d state=%s', y, prob, state)
      T[t][y] = prob
      newpath[y] = path[state].concat(y)
    }
    // console.log('t=%d T=%j', t, T)
    path = newpath
    console.log('t=%d path=%j', t, path)
  }
  let {max:prob, index:si} = argmax(states.map((y)=>T[obs.length - 1][y]))
  console.log('T=%j', T)
  return {prob, path:path[states[si]]}
}

let {prob, path} = viterbi('喵 喵 汪'.split(' '), ['N', 'V'], P)
console.log('prob=%d path=%j＝最可能的隱序列', prob, path)
```

## 觀念

* [維基百科:維特比演算法](https://zh.wikipedia.org/wiki/%E7%BB%B4%E7%89%B9%E6%AF%94%E7%AE%97%E6%B3%95)
* [自然語言處理 -- Hidden Markov Model](https://ckmarkoh.github.io/blog/2014/04/03/natural-language-processing-hidden-markov-models/)
* [自然語言處理 -- Viterbi Algorithm](https://ckmarkoh.github.io/blog/2014/04/06/natural-language-processing-viterbi-algorithm/)

## 實作

* https://github.com/miguelmota/hidden-markov-model
* https://github.com/123jimin/hmm.js/blob/master/hmm.js
* https://github.com/123jimin/hmm.js/tree/master







 

