# HackCPU 延伸指令集

## 基本運算延伸

```
D << AM // 左移
D >> AM // 右移
D * AM // 乘法
D / AM // 除法
D % AM // 餘數
D < AM // 小於
D <= AM // 小於或等於
D > AM // 大於
D >= AM // 大於或等於
D == AM // 等於
D != AM // 不等於
D ^ AM // xor
```

## 軟體中斷延伸

swi 是軟體中斷 Software Interrupt 的簡稱，swi 會根據暫存器 A 的內容決定要做甚麼動作。

舉例而言，swi 0 會印出暫存器 D 中的整數，意思是下列程式會印出 374

```
@374
D=A
@0
swi
```

HackCPU 的延伸指令集包含一組預先定義好的 swi，像是 swi 0 是印出整數， swi 16 是設定浮點數。

有了 swi ，我們可以定義一些巨集運算，以下是HackCPU 的延伸指令集所支援的預設巨集運算：

```
// 列印功能
iput = @0;swi // 印出整數 
cput = @1;swi // 印出字元
sput = @%s;D=A;@3;swi // 印出字串

// 浮點數功能
巨集   = 展開內容
fput   = @18;swi
fset t = @t;D=A;@16;swi // 將 t 位置的兩格記憶體設定給 f 
fget t = @t;D=A;@16;swi // 取回 f 並放入 t 位置的兩格記憶體 
fadd t = @t;D=A;@19;swi // f = f + t
fsub t = @t;D=A;@20;swi // f = f - t
fmul t = @t;D=A;@21;swi // f = f * t
fdiv t = @t;D=A;@22;swi // f = f / t
```

延伸版的 HackCPU 浮點數 f 被映射到位址 m[24577..24578]，以 32 位元浮點數表示，緊接在鍵盤暫存器的後面。

所以我們可以用 @24577; D=M 取得 f 的前 16bit，然後用  @24578; D=M  取得 f 的後 16bit。(如果有需要的話！)
