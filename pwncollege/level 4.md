
## semaphores 
`&data + 4 + index`


## ypu fds
`&data + 4*index + 3200`

## mmap 
`memory[2*index+1600]`


## load program
`&data + 768 * index` -> no sem

## init ypu
```
sem_wait((sem_t *)&data + ypu_index + 384);
memcpy((void *)mmaped_memory[2 * ypu_index + 1600], (char *)&data + 768 * index, 0x1000uLL);
sem_post((sem_t *)&data + ypu_index + 384);
```

## run ypu
```
sem_wait((sem_t *)&data + ypu_index + 384);
ioctl(*((_DWORD *)&data + 4 * ypu_index + 3200), 0x539uLL, 0LL);
sem_post((sem_t *)&data + ypu_index + 384);
```