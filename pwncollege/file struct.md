
![[Pasted image 20260302151922.png]]
https://elixir.bootlin.com/glibc/glibc-2.31/source/libio/bits/types/struct_FILE.h#L49

https://elixir.bootlin.com/glibc/glibc-2.31/source/libio/libio.h#L62

```
int challenge()
{
  int result; // eax
  unsigned int v1; // [rsp+20h] [rbp-120h]
  unsigned int v2; // [rsp+20h] [rbp-120h]
  unsigned int v3; // [rsp+20h] [rbp-120h]
  unsigned int v4; // [rsp+20h] [rbp-120h]
  unsigned int v5; // [rsp+20h] [rbp-120h]
  unsigned int v6; // [rsp+20h] [rbp-120h]
  unsigned int size; // [rsp+24h] [rbp-11Ch]
  size_t nbytes[6]; // [rsp+30h] [rbp-110h] BYREF
  void *ptr[10]; // [rsp+60h] [rbp-E0h] BYREF
  char s1[136]; // [rsp+B0h] [rbp-90h] BYREF
  unsigned __int64 v11; // [rsp+138h] [rbp-8h]

  v11 = __readfsqword(0x28u);
  memset(ptr, 0, sizeof(ptr));
  memset(nbytes, 0, 40);
  create_tmp_file();
  while ( 1 )
  {
    while ( 1 )
    {
      while ( 1 )
      {
        while ( 1 )
        {
          while ( 1 )
          {
            while ( 1 )
            {
              while ( 1 )
              {
                while ( 1 )
                {
                  while ( 1 )
                  {
                    while ( 1 )
                    {
                      while ( 1 )
                      {
                        printf(
                          "[*] Commands: (new_note/del_note/write_note/read_note/open_file/close_file/read_file/write_fil"
                          "e/write_fp/open_flag/quit):\n"
                          "> ");
                        __isoc99_scanf("%127s%*c", s1);
                        puts(&byte_3466);
                        if ( strcmp(s1, "new_note") )
                          break;
                        printf("Which note? (0-10)\n> ");
                        __isoc99_scanf("%127s%*c", s1);
                        v1 = atoi(s1);
                        printf("How many bytes to the note?\n> ");
                        __isoc99_scanf("%127s%*c", s1);
                        size = atoi(s1);
                        ptr[v1] = malloc(size);
                        *((_DWORD *)nbytes + v1) = size;
                        printf("notes[%d] = %p;", v1, ptr[v1]);
                      }
                      if ( strcmp(s1, "del_note") )
                        break;
                      printf("Which note? (0-10)\n> ");
                      __isoc99_scanf("%127s%*c", s1);
                      v2 = atoi(s1);
                      printf("free(notes[%d]);\n", v2);
                      free(ptr[v2]);
                      ptr[v2] = 0LL;
                    }
                    if ( strcmp(s1, "write_note") )
                      break;
                    printf("Which note? (0-10)\n> ");
                    __isoc99_scanf("%127s%*c", s1);
                    v3 = atoi(s1);
                    read(0, ptr[v3], *((unsigned int *)nbytes + v3));
                  }
                  if ( strcmp(s1, "read_note") )
                    break;
                  printf("Which note? (0-10)\n> ");
                  __isoc99_scanf("%127s%*c", s1);
                  v4 = atoi(s1);
                  read(1, ptr[v4], *((unsigned int *)nbytes + v4));
                }
                if ( strcmp(s1, "open_file") )
                  break;
                fp = fopen("/tmp/babyfile.txt", "r+");
                printf("fp = fopen(\"/tmp/babyfile.txt\", \"r+\") = %p\n", fp);
              }
              if ( strcmp(s1, "close_file") )
                break;
              fclose(fp);
            }
            if ( strcmp(s1, "write_file") )
              break;
            printf("Which note? (0-10)\n> ");
            __isoc99_scanf("%127s%*c", s1);
            v5 = atoi(s1);
            printf("fwrite(notes[%d], %d, %d, fp);\n", v5, 1LL, *((unsigned int *)nbytes + v5));
            fwrite(ptr[v5], 1uLL, *((unsigned int *)nbytes + v5), fp);
          }
          if ( strcmp(s1, "read_file") )
            break;
          printf("Which note? (0-10)\n> ");
          __isoc99_scanf("%127s%*c", s1);
          v6 = atoi(s1);
          printf("fread(notes[%d], %d, %d, fp);\n", v6, 1LL, *((unsigned int *)nbytes + v6));
          fread(ptr[v6], 1uLL, *((unsigned int *)nbytes + v6), fp);
        }
        if ( strcmp(s1, "write_fp") )
          break;
        print_fp(fp);
        read(0, fp, 0x1E0uLL);
        print_fp(fp);
      }
      if ( strcmp(s1, "open_flag") )
        break;
      fopen("/tmp/babyflag.txt", "r+");
    }
    result = strcmp(s1, "quit");
    if ( !result )
      break;
    puts("Unrecognized choice!\n");
  }
  return result;
}
```