
![[Pasted image 20260527095639.png]]

The “P” flag is confusing because it really belongs to the _previous_ chunk. It indicates that the previous chunk is a _free_ chunk. This means when _this_ chunk is freed, it can be safely joined onto the previous chunk to create a much larger free chunk.

![[Pasted image 20260527102615.png]]

[Overview of GLIBC heap exploitation techniques](https://0x434b.dev/overview-of-glibc-heap-exploitation-techniques/)

[shellphish/how2heap: A repository for learning various heap exploitation techniques.](https://github.com/shellphish/how2heap/tree/master)