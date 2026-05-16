
opening the device makes it allocate 1MB of data in the kernel that is user accessible
```
__int64 __fastcall device_open(inode *inode, file *file)
{
  _QWORD *v2; // rbx
  __int64 result; // rax

  v2 = (_QWORD *)kvmalloc_node(16LL, 3520LL, 0xFFFFFFFFLL);
  *v2 = vmalloc_user(0x100000LL);
  v2[1] = kvmalloc_node(0x100000LL, 3520LL, 0xFFFFFFFFLL);
  result = 0LL;
  file->private_data = v2;
  return result;
}
```

mmap allows us to access this memory in userspace
```
__int64 __fastcall device_mmap(file *file, vm_area_struct *vma)
{
  return (unsigned int)((int)remap_vmalloc_range(vma, *(_QWORD *)file->private_data, 0LL) >> 31);
}
```


Instructions 

```
imm - 0x20  
add - 0x1
stk - 0x40
stm - 0x8
sys - 0x4
cmp - 0x2
ldm - 0x80
jmp - 0x10
```

Syscalls

```
open - 0x8
read - 0x20
exec - 0x40

```

Registers

```
a - 0x20
b - 0x40
c - 0x8
d - 0x2
s - 0x4
i - 0x1
f - 0x10
ds - 0x80
```

Order:
```
[opcode] [arg1] [arg2]
```


Vulnerable function:

```
void __fastcall sys_exec(vmstate_t *state, word_t addr_reg_a)
{
  __int64 memory_byte; // rdx
  word_t memory_byte_; // cl
  unsigned __int8 *code_base; // rax
  word_t new_i; // al

  memory_byte = state->memory[4096 * (unsigned __int64)state->regs.ds + addr_reg_a];
  memory_byte_ = state->memory[4096 * (unsigned __int64)state->regs.ds + addr_reg_a];
  code_base = &state->code->op + 4096 * memory_byte;
  if ( *(_DWORD *)code_base == 5591129 && state->memlimit > addr_reg_a )
  {
    *(_QWORD *)&state->regs.a = 0LL;
    state->regs.ds = 0;
    new_i = code_base[0x2000 * memory_byte + 4];
    state->regs.cs = memory_byte_;
    state->regs.i = new_i;
  }
}
```

using reg_a we can control which byte is read into `memory_byte`, this variable is then used as a offset to the new code base, accessing it and putting it in the cache:

`code_base = &state->code->op + 4096 * memory_byte;`


plan:
open flag
read flag
call exec with different bytes of flag
flush and reload


```
ffffffffc0000000 t device_release       [challenge]
ffffffffc0000040 t device_open  [challenge]
ffffffffc0000090 t device_mmap  [challenge]
ffffffffc00008c0 t device_ioctl [challenge]
ffffffffc0000a10 t cleanup_module       [challenge]
ffffffffc0000540 t interpret_stk        [challenge]
ffffffffc00002e0 t sys_read     [challenge]
ffffffffc00001b0 t describe_flags       [challenge]
ffffffffc00006a0 t interpret_jmp        [challenge]
ffffffffc00006d0 t interpret_sys        [challenge]
ffffffffc00004c0 t write_memory [challenge]
ffffffffc00009c0 t init_module  [challenge]
ffffffffc00004a0 t read_memory  [challenge]
ffffffffc00003e0 t read_register        [challenge]
ffffffffc0000350 t sys_sleep    [challenge]
ffffffffc0000250 t sys_open     [challenge]
ffffffffc0000130 t describe_instruction [challenge]
ffffffffc00005c0 t interpret_stm        [challenge]
ffffffffc0000500 t interpret_add        [challenge]
ffffffffc0000360 t load_header  [challenge]
ffffffffc0000240 t crash        [challenge]
ffffffffc0000640 t interpret_cmp        [challenge]
ffffffffc0000600 t interpret_ldm        [challenge]
ffffffffc00004e0 t interpret_imm        [challenge]
ffffffffc0000390 t sys_exec     [challenge]
ffffffffc00000b0 t describe_register    [challenge]
ffffffffc0000340 t sys_exit     [challenge]
ffffffffc0000440 t write_register       [challenge]
ffffffffc00007f0 t interpret_instruction        [challenge]
```