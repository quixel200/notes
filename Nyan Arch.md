

## registers 

a - 0x10
b - 0x20 
c - 0x30
instruction register(i) - 0x1
# memory region 

map 0x100 bytes, first 4 bytes will be used to store the register values 
0x1 - a 
0x2 - b 
0x3 - c 
0x4 - i 

## instructions 

mov register,constant - move a constant value into the register 
load register(points to memory),register(value) - loads value into memory 
xor reg1,reg2 (reg1 = reg1 ^ reg2)
syscall  syscall_number reg 
(reg will be register that the return value goes to)
syscall numbers -
0x1 - open
0x2 - read 
0x3 - write 
0x4 - exit 

values will be passed to the sycalls using the registers, for eg:
open(a,b) 

a and b being pointers to the memory region 