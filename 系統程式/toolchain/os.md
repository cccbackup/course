# 作業系統 - os

## os01 -- 時間中斷

* https://github.com/cccbook/c2verilog/blob/master/src/os/01/os01.mx

```
user@DESKTOP-96FRN6B MSYS /d/ccc/book/c2verilog/src
$ make os01
../bin/ma2 os/01/os01.mx -o os/01/os01.sx
../bin/as3 os/01/os01
../bin/vm3 os/01/os01.ox
hello
Thu Apr 11 11:46:23 2019
hello
Thu Apr 11 11:46:25 2019
hello
Thu Apr 11 11:46:28 2019
hello
Thu Apr 11 11:46:30 2019
make: *** [Makefile:80: os01] Interrupt

```

## os02 -- 區分模組

* https://github.com/cccbook/c2verilog/tree/master/src/os/02

```
user@DESKTOP-96FRN6B MSYS /d/ccc/book/c2verilog/src
$ make os02
Makefile:83: warning: overriding recipe for target 'os02'
Makefile:46: warning: ignoring old recipe for target 'os02'
../bin/ma2 os/02/boot.mx os/02/const.mx os/02/time.mx -o os/02/os02.sx
../bin/as3 os/02/os02
../bin/vm3 os/02/os02.ox
timerHandler: time=Thu Apr 11 11:48:37 2019

timerHandler: time=Thu Apr 11 11:48:38 2019

timerHandler: time=Thu Apr 11 11:48:38 2019

timerHandler: time=Thu Apr 11 11:48:39 2019

timerHandler: time=Thu Apr 11 11:48:40 2019

timerHandler: time=Thu Apr 11 11:48:40 2019

timerHandler: time=Thu Apr 11 11:48:41 2019

make: *** [Makefile:85: os02] Interrupt

```


