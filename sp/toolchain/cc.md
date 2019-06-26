# 編譯器 - cc

## 執行

```
$ make cRun file=sum
../bin/cc2 ../test/c/sum
../bin/ma2 ../test/c/sum.mx -o ../test/c/sum.sx
../bin/as3 ../test/c/sum
../bin/vm3 ../test/c/sum.ox
55
```

## 輸入檔

* https://github.com/cccbook/c2verilog/blob/master/test/c/sum.cx

```c

s=0;
i=1;
while (i <= 10) {
  s = s + i;
  i = i + 1;
}
asm(".puti s");
```

## 輸出檔

* https://github.com/cccbook/c2verilog/blob/master/test/c/sum.mx

```
.setc t1 = 0
.set  s = t1
.setc t1 = 1
.set  i = t1
(L1)
.set  t1 = i
.setc t2 = 10
.op   t3 = t1 <= t2
.ifnot t3 goto L2
.set  t1 = s
.set  t2 = i
.op   t3 = t1 + t2
.set  s = t3
.set  t1 = i
.setc t2 = 1
.op   t3 = t1 + t2
.set  i = t3
.goto L1
(L2)
.puti s

```
