
gadget to delay execution and speculate?

```
00                 public gadget
.text:0000000000000000 gadget          proc near               ; DATA XREF: device_ioctl+71↓o
.text:0000000000000000                 movsx   rax, byte ptr [rdi]
.text:0000000000000004                 shl     rax, 0Ch
.text:0000000000000008                 movsx   eax, byte ptr [rsi+rax]
.text:000000000000000C                 retn
.text:000000000000000C gadget          endp
```

```
__int64 __fastcall device_ioctl(file *file, unsigned int cmd, unsigned __int64 arg)
{
  char *flag; // rdx
  char *private_data; // rbp
  unsigned __int64 user_space; // r12
  int flag_4_bytes; // ecx
  unsigned int mangle_something_idk; // eax
  int user_space_1; // r13d
  int some_counter; // ebx
  __int64 result; // rax
  uint64_t *target; // [rsp+8h] [rbp-38h] BYREF
  unsigned __int64 v12; // [rsp+10h] [rbp-30h]

  flag = ::flag;
  private_data = (char *)file->private_data;
  v12 = __readgsqword(0x28u);
  user_space = (unsigned __int8)*private_data;
  do
  {
    flag_4_bytes = *(_DWORD *)flag;
    flag += 4;
    mangle_something_idk = ~flag_4_bytes & (flag_4_bytes - 16843009) & 0x80808080;
  }
  while ( !mangle_something_idk );
  if ( (~flag_4_bytes & (flag_4_bytes - 16843009) & 0x8080) == 0 )
  {
    mangle_something_idk >>= 16;
    flag += 2;
  }
  if ( user_space > flag - &::flag[__CFADD__((_BYTE)mangle_something_idk, (_BYTE)mangle_something_idk) + 3] )
  {
    result = -1LL;
  }
  else
  {
    target = (uint64_t *)gadget;
    user_space_1 = (unsigned __int8)private_data[1];
    some_counter = 0;
    if ( private_data[1] )
    {
      do
      {
        victim(&safe_flag[user_space], private_data, 0LL, (uint64_t *)&target);
        ++some_counter;
      }
      while ( user_space_1 != some_counter );
    }
    target = (uint64_t *)safe;
    _mm_mfence();
    victim(&::flag[user_space], private_data, 0LL, (uint64_t *)&target);
    result = 0LL;
  }
  if ( __readgsqword(0x28u) != v12 )
    return init_module();
  return result;
}
```

victim function
```
__int64 __fastcall victim(char *safe_flag, char *private_data, __int64 input, uint64_t *target)
{
  volatile int junk; // [rsp+4h] [rbp-1Ch]

  _mm_clflush(target);
  _mm_mfence();
  return junk & ((unsigned int (__fastcall *)(char *, char *, __int64))*target)(safe_flag, private_data, input);
}
```

disassembly:
```
 public victim
.text:0000000000000090 victim          proc near               ; CODE XREF: device_ioctl+9B↓p
.text:0000000000000090                                         ; device_ioctl+C6↓p
.text:0000000000000090
.text:0000000000000090 result          = dword ptr -20h
.text:0000000000000090 junk            = dword ptr -1Ch
.text:0000000000000090
.text:0000000000000090                 push    r12
.text:0000000000000092                 mov     r12, rsi
.text:0000000000000095                 push    rbp
.text:0000000000000096                 mov     rbp, rdi
.text:0000000000000099                 push    rbx
.text:000000000000009A                 mov     rbx, rcx
.text:000000000000009D                 sub     rsp, 8
.text:00000000000000A1                 clflush byte ptr [rcx]
.text:00000000000000A4                 mfence
.text:00000000000000A7                 mov     rdi, rbp
.text:00000000000000AA                 mov     rsi, r12
.text:00000000000000AD                 call    qword ptr [rbx]
.text:00000000000000AF                 mov     ebx, eax
.text:00000000000000B1                 mov     [rsp+20h+result], ebx
.text:00000000000000B4                 mov     eax, [rsp+20h+result]
.text:00000000000000B7                 mov     edx, [rsp+20h+junk]
.text:00000000000000BB                 add     rsp, 8
.text:00000000000000BF                 pop     rbx
.text:00000000000000C0                 pop     rbp
.text:00000000000000C1                 and     eax, edx
.text:00000000000000C3                 pop     r12
.text:00000000000000C5                 retn
.text:00000000000000C5 victim          endp
```

this is probably the exploit `call    qword ptr [rbx]`

device open:

```
__int64 __fastcall device_open(inode *inode, file *file)
{
  file->private_data = (void *)vmalloc_user(0x100000LL);
  return 0LL;
}
```

the mangle is just an optimized implementation of strlen
index 0 - flag index
index 1 - number of rounds to speculate (run safe gadget)