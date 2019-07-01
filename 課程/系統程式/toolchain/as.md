# 組譯器 - as

## 執行

```
user@DESKTOP-96FRN6B MSYS /d/ccc/book/c2verilog/src
$ make sRun file=sum
../bin/as3 ../test/m/sum
../bin/vm3 ../test/m/sum.ox
sum=55

```

## 輸入檔

* https://github.com/cccbook/c2verilog/blob/master/test/m/sum.sx

```
// =========== iFile: ../test/c/sum.mx ==============
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
// .set  t1 = i 
@i
D=M
@t1
M=D
// .setc t2 = 10 
@10
D=A
@t2
M=D
// .op   t3 = t1 <= t2 
@t1
D=M
@t2
D=D<=M
@t3
M=D
// .ifnot t3 goto L2 
@t3
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
// .puti s 
@s
D=M
@0
swi

```

## 輸出檔

請先執行上述的 `make sRun file=sum` 指令後會產生出來，該檔是二進位，請在 Visual Studio Code 中安裝 hexdump for VSCode ，然後在該檔案 (例如 sum.ox) 上按滑鼠右鍵選 Show Hexdump 檢視之：

```
  Offset: 00 01 02 03 04 05 06 07 08 09 0A 0B 0C 0D 0E 0F 	
00000000: 09 00 87 EA 73 00 75 00 6D 00 3D 00 00 00 0D 00    ...js.u.m.=.....
00000010: 00 00 00 00 10 EC FF 3F 08 E3 FF 3F 10 FC FE 3F    .....l.?.c.?.|~?
00000020: 08 E3 01 00 10 EC FF 3F 08 E3 FF 3F 10 FC FD 3F    .c...l.?.c.?.|}?
00000030: 08 E3 FD 3F 10 FC FC 3F 08 E3 0A 00 10 EC FB 3F    .c}?.||?.c...l{?
00000040: 08 E3 FC 3F 10 FC FB 3F 90 F9 FA 3F 08 E3 FA 3F    .c|?.|{?.yz?.cz?
00000050: 10 FC 51 00 02 E3 FE 3F 10 FC FF 3F 08 E3 FD 3F    .|Q..c~?.|.?.c}?
00000060: 10 FC FC 3F 08 E3 FF 3F 10 FC FC 3F 90 F0 FB 3F    .||?.c.?.||?.p{?
00000070: 08 E3 FB 3F 10 FC FE 3F 08 E3 FD 3F 10 FC FF 3F    .c{?.|~?.c}?.|.?
00000080: 08 E3 01 00 10 EC FC 3F 08 E3 FF 3F 10 FC FC 3F    .c...l|?.c.?.||?
00000090: 90 F0 FB 3F 08 E3 FB 3F 10 FC FD 3F 08 E3 19 00    .p{?.c{?.|}?.c..
000000a0: 87 EA 02 00 10 EC 03 00 C0 EB FE 3F 10 FC 00 00    .j...l..@k~?.|..
000000b0: C0 EB 07 00 10 EC 03 00 C0 EB                      @k...l..@k

```

