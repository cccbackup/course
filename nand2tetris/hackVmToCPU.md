# 將 HackVM 對應到 HackCPU

暫存器 -- SP:R0, LCL:R1, ARG:R2, THIS:R3, THAT:R4, TEMP:R5-12, General Purpose:R13..15

Static -- static: mapped on RAM[16 ... 255];

each segment reference static i appearing in a VM file named f is compiled to the assembly language symbol f.i (recall that the assembler further maps such symbols to the RAM, from address 16 onward)

