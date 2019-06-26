# 在 windows 中類似於 linux 的環境

1. MSYS2 -- http://www.msys2.org/
    * https://www.emdalo.com/posts/risc-v-gnu-compiler-toolchain-howto-compile-on-windows/
2. Choco -- 
    * https://guangchuangyu.github.io/cn/2018/06/chocolatey/
3. Ubuntu Linux in Windows
    * https://blog.gtwang.org/windows/how-to-get-ubuntu-and-bash-running-on-windows-10/
4. 安裝虛擬機 (VirtualBox, VMWare, Docker Machine, ...)
    * Docker Machine 需要 Microsoft Windows 10 Professional or Enterprise 才行， Home Edition 不行！ 
    * 然後再安裝 Linux

## MSYS

MSYS 的進入目錄 home 在 C:\msys64\home\user

在 MSYS 中使用 cd /c 就會切到 c 磁碟 ....

```
user@DESKTOP-96FRN6B MSYS ~
$ cd /d
user@DESKTOP-96FRN6B MSYS /d
...
user@DESKTOP-96FRN6B MSYS /d/ccc/book/sp/code/c
$ cd 10-thread/

user@DESKTOP-96FRN6B MSYS /d/ccc/book/sp/code/c/10-thread
$ ls
deadlock.c  georgeMary.c  mutex1.c  norace.c  race.c  README.md  webserver.c

user@DESKTOP-96FRN6B MSYS /d/ccc/book/sp/code/c/10-thread
$ gcc georgeMary.c -o georgeMary


user@DESKTOP-96FRN6B MSYS /d/ccc/book/sp/code/c/10-thread
$

user@DESKTOP-96FRN6B MSYS /d/ccc/book/sp/code/c/10-thread
$ ./georgeMary
George
Mary
----------------
George
----------------
----------------
George
Mary

```

## 嵌入式

* https://gnu-mcu-eclipse.github.io/



