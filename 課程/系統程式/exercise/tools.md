# Nand2tetris 作業操作方法

```
$ git clone https://github.com/ccckmit/co106a.git
// 加入或修改你的作業習題，例如 Not.hdl
$ git add -A
$ git commit -m "finish Not.hdl"
$ git push origin master
```

## Nand2tetris 軟體安裝

* Windows 版 -- after downloading, put the downloaded zip file in an empty directory on your computer, and extract its contents as is, without changing the directories structure and names.

## 軟體用法

* https://www.nand2tetris.org/software
* Mac 版 -- 請參考 https://www.nand2tetris.org/copy-of-nestedcall-1

下載 https://www.nand2tetris.org/software 中的

* Download the Nand2tetris Software Suite Version 2.6 (about 730K).

然後解壓縮，接著到 tools 資料夾中，進行下列動作

```
// 確認電腦中是否有安裝 java
csienqu-teacher:tools csienqu$ java -version
java version "1.8.0_65"
Java(TM) SE Runtime Environment (build 1.8.0_65-b17)
Java HotSpot(TM) 64-Bit Server VM (build 25.65-b01, mixed mode)
// 將 HardwareSimulator.sh 改成可執行模式，並執行之
csienqu-teacher:tools csienqu$ chmod 777 HardwareSimulator.sh
csienqu-teacher:tools csienqu$ ./HardwareSimulator.sh
```

後續的軟體使用請參考 [Hardware Simulator Tutorial](https://docs.wixstatic.com/ugd/44046b_bfd91435260748439493a60a8044ade6.pdf)
