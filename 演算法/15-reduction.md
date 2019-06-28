## 轉換化約法 Reduction 

Reduction 是將某問題轉換為另一問題後再求解，然後再將解答轉換回原問題的方法！

### 簡易範例

舉例而言，假如我們不知道怎麼做乘法 (a*b) ，但是卻知道怎麼做平方 (a^2)， 那麼我們可以透過下列方程式，將乘法的計算轉為平方的計算。

$`(a+b)^2 = a^2 + 2ab + b^2`$

$`2ab = (a+b)^2 - a^2 - b^2`$

$`ab = ((a+b)^2 - a^2 - b^2)/2`$

於是我們就可以透過計算 $`((a+b)^2 - a^2 - b^2)/2`$ 這個式子來計算乘法。


### SAT 問題

學程式的人通常已經熟悉了布林代數式，以下是一些布林代數式的範例

```
x | y

x & y

!x | y

(x|y) & (x) & (!y)

```

對於某個布林代數式 B(x,y,...)，如果帶入某組值後 (例如 x=1, y=0, ...)，會使得該布林代數式 B(x,y, ...) = 1，那麼我們就稱該組滿足了 B。
 
SAT (Satisfiability) 就是在問布林代數式是否能被滿足的一個問題，希望我們能設計出一個演算法，假如 B 能被滿足，那麼就傳回 1，無法滿足時就傳回 0。

### 將 SAT 問題轉換為『整數規劃』問題

假如我們想尋找滿足某布林代數式 B 的解答，但是我們只會解『整數規劃』，那麼我們可以把布林代數式重寫成整數規劃方程式，這樣就可以用整數規劃算法求解布林代數式 B 的解答了。

以下是一個範例：

B = (x|y) & (!x) & (!y|x)

轉換成整數規劃

```
maximize E = (x+y)*(1-x)*((1-y)+x)

x + y >= 1
(1-x) >= 1
((1-y)+x) >= 1

x, y 為二進位整數 (0, 1)
 
```

這樣只要找到 E >= 1 的解答，就等於找到滿足布林代數式 B 的解答了！

### NP-Complete 問題

1971 年 Stephen Cook 在以下論文中提出了一個驚人的定理，震撼了整個『資訊科學』領域。

> Cook, Stephen (1971). ["The complexity of theorem proving procedures"](http://portal.acm.org/citation.cfm?coll=GUIDE&dl=GUIDE&id=805047). Proceedings of the Third Annual ACM Symposium on Theory of Computing. pp. 151–158. doi:10.1145/800157.805047.

該論文證明了後來被稱為 Cook–Levin theorem 的定理，提出了一類稱為 NP-Complete 的問題，後來 Leonid Levin 找到幾十個這類的 NP-Complete 問題，因此該定理被稱為 Cook–Levin theorem 。

Cook 的證明就是利用將『非確定圖靈機』的執行轉化為 SAT 問題，進而把所有『非確定圖靈機』在多項式時間內可解的問題，通通在多項式時間內轉化成 SAT 問題的方法，證明了所有 NP 問題都可以 reduce 成 SAT 問題。

要進一步了解該證明請參考 https://en.wikipedia.org/wiki/Cook%E2%80%93Levin_theorem

