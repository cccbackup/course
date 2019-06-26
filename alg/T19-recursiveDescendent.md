# 第 19 章 - 遞迴下降法 Recursive Descendent 

遞迴下降法是用來《剖析語言》的一種方法，經常被用在《編譯器、自然語言處理》等領域。

要了解遞迴下降法必須先了解 BNF/EBNF 語法，請先閱讀以下文章！

* [語法理論 (Medium)](https://medium.com/%E4%BA%BA%E5%B7%A5%E6%99%BA%E6%85%A7/%E8%AA%9E%E6%B3%95%E7%90%86%E8%AB%96-23bc87126e6)

關於《語言處理技術》更詳細的內容請參考我寫的以下書籍！

* [電子書：語言處理技術 (SlideShare)](https://www.slideshare.net/ccckmit/ss-15898210)

我們可以用《遞迴下降法》來產生語句，或者撰寫《編譯器程式》！

## 自動產生語句

* <https://pdos.csail.mit.edu/archive/scigen/>

接著請想想，這種程式該怎麼做呢？

讓我們用一個更簡單的例子示範，那就是自動產生數學運算式。

檔案： https://github.com/cccbook/algjs/blob/master/code/19-recursiveDescendent/genexp1.js

```
var R = require('./random')

// === BNF Grammar =====
// E = T [+-*/] E | T
// T = [0-9] | (E)

function print(s) {
  process.stdout.write(s);
}

function E() {
  if (R.randInt(1,10) <= 5) {
    T(); print(R.randChar("+-*/")); E();
  } else {
    T();
  }
}

function T() {
  if (R.randInt(1,10) < 7) {
    print(R.randChar("0123456789"));
  } else {
    print("("); E(); print(")");
  }
}

for (var i=0; i<10; i++) {
  E();
  print("\n");
}
```

執行結果

```
nqu-192-168-61-142:code mac020$ node genexp
4
0/0+(2)*9
4-(9)*((((3*(4))-(8))+(0)+8/(8)+2)+2/6)
3/(((((1*8+6)))))*((6/4/3))/(((2+9))+(((2))+8/((4*(5))*2))/4)
(1+(1))-((7))
(2+(((4))))+(5)
((1/(((3+(7)-(4-1)/9*8/7-6)/(4)-3+3)-6-9*(((2+(((6*4/4)))*(8/3))))-9-0-1+5*8*((5)/(3)-1/(1)-9)+(5+5*5))))*5/2
8
1
(0)*7
```

## 編譯數學運算式為中間碼

檔案： https://github.com/cccbook/algjs/blob/master/code/19-recursiveDescendent/compileExp.js

```js
/* 語法
E = T ([+-/*] E)*
T = N | (E)

範例：3+(5*4)-2
*/

var c = console;

var tagMap={
  N : ["0", "1", "2", "3", "4", "5", "6", "7", "8", "9"],
  OP: ["+", "-", "*", "-"]
};

var wi = 0;

function isNext(tag) {
  if (words[wi] === tag) return true;
  var tagWords=tagMap[tag];
  if (typeof tagWords === "undefined") 
    return false;
  else
    return (tagWords.indexOf(words[wi])>=0);
}

function next(tag) {
  c.log("tag="+tag+" word="+words[wi]);
  if (isNext(tag)) {
    return words[wi++];
  }
  throw Error("Error !");
}

var tempIdx = 0;
var getTemp=function() {
    return tempIdx++;
}
// E = T ([+-/*] E)*
function E() {
  var t = T();
  while (isNext("OP")) {
    var op = next("OP");
    var e = E();
    var result = getTemp();
    console.log(" T%d=T%d%sT%d", result, t, op, e);
    t = result;
  }
  return t;
}

// T = N | (E)
function T() {
  if (isNext("N")) {
    var t = getTemp();
    var number = next("N");
    console.log(" T%d=%d", t, number);
    return t;
  } else {
    next("(");
    var e = E();
    next(")");
    return e;
  }
}

var words="3+(5*4)-2";
c.log("%j", words);
E(words);
```

執行

```
$ node compileExp
"3+(5*4)-2"
tag=N word=3
 T0=3
tag=OP word=+
tag=( word=(
tag=N word=5
 T1=5
tag=OP word=*
tag=N word=4
 T2=4
 T3=T1*T2
tag=) word=)
tag=OP word=-
tag=N word=2
 T4=2
 T5=T3-T4
 T6=T0+T5
```
