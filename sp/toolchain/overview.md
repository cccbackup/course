# 工具鏈 -- tc

```
user@DESKTOP-96FRN6B MSYS /d/ccc/book/c2verilog/src
$ make clean
rm -f ../bin/*.o ../bin/*.exe

user@DESKTOP-96FRN6B MSYS /d/ccc/book/c2verilog/src
$ make
gcc -std=c99 -O0 -Wall  cc/2/cc.c cc/2/lexer.c cc/2/compiler.c ir/2/ir.c ir/2/irvm.c ir/2/ir2m.c lib/util.c lib/map.c lib/strTable.c -o ../bin/cc2
gcc -std=c99 -O0 -Wall  ma/2/macro.c lib/util.c lib/map.c lib/strTable.c -o ../bin/ma2
gcc -std=c99 -O0 -Wall  as/3/asm.c lib/util.c lib/map.c lib/strTable.c -o ../bin/as3
gcc -D_VM_EXT_ -g -std=c99 -O0 -Wall  vm/3/vm.c lib/util.c lib/map.c lib/strTable.c -o ../bin/vm3

user@DESKTOP-96FRN6B MSYS /d/ccc/book/c2verilog/src
$ make cRun file=sum
../bin/cc2 ../test/c/sum
../bin/ma2 ../test/c/sum.mx -o ../test/c/sum.sx
../bin/as3 ../test/c/sum
../bin/vm3 ../test/c/sum.ox
55

```