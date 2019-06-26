# 巨集處理器 - ma

## 執行

```
user@DESKTOP-96FRN6B MSYS /d/ccc/book/c2verilog/src
$ make mRun file=sum
../bin/ma2 ../test/m/sum.mx -o ../test/m/sum.sx
../bin/as3 ../test/m/sum
../bin/vm3 ../test/m/sum.ox
sum=55

```

## 輸入檔

* https://github.com/cccbook/c2verilog/blob/master/test/c/sum.mx

```
@main  
0;JMP  

(msg) "sum=", 0
(lineEnd) 13, 0

(main)
.setc t1 = 0
.set  s = t1
.setc t1 = 1
.set  i = t1
(L1)
.set  t2 = i
.setc t3 = 10
.op   t4 = t2 <= t3
.ifnot t4 goto L2
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
.puts msg
.puti s
.puts lineEnd
```

## 輸出檔

* https://github.com/cccbook/c2verilog/blob/master/test/c/sum.sx

```
// =========== iFile: ../test/m/sum.mx ==============
@main    
0;JMP    
  
(msg) "sum=", 0  
(lineEnd) 13, 0  
  
(main)  
// .setc t1 = 0  
@0
D=A
@t1
M=D
// .set  s = t1  
@t1
D=M
@s
M=D
// .setc t1 = 1  
@1
D=A
@t1
M=D
// .set  i = t1  
@t1
D=M
@i
M=D
(L1)  
// .set  t2 = i  
@i
D=M
@t2
M=D
// .setc t3 = 10  
@10
D=A
@t3
M=D
// .op   t4 = t2 <= t3  
@t2
D=M
@t3
D=D<=M
@t4
M=D
// .ifnot t4 goto L2  
@t4
D=M
@L2
D;JEQ
// .set  t1 = s  
@s
D=M
@t1
M=D
// .set  t2 = i  
@i
D=M
@t2
M=D
// .op   t3 = t1 + t2  
@t1
D=M
@t2
D=D+M
@t3
M=D
// .set  s = t3  
@t3
D=M
@s
M=D
// .set  t1 = i  
@i
D=M
@t1
M=D
// .setc t2 = 1  
@1
D=A
@t2
M=D
// .op   t3 = t1 + t2  
@t1
D=M
@t2
D=D+M
@t3
M=D
// .set  i = t3  
@t3
D=M
@i
M=D
// .goto L1  
@L1
0;JMP
(L2)  
// .puts msg  
@msg
D=A
@3
swi
// .puti s  
@s
D=M
@0
swi
// .puts lineEnd
@lineEnd
D=A
@3
swi

```
