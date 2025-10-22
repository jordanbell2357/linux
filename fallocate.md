# fallocate

<https://man7.org/linux/man-pages/man1/fallocate.1.html>

> fallocate is used to manipulate the allocated disk space for a file, either to deallocate or preallocate it.
> For filesystems which support the fallocate(2) system call, preallocation is done quickly by allocating blocks
> and marking them as uninitialized, requiring no IO to the data blocks. This is much faster than creating a file by filling it with zeroes.

```console
ubuntu@LAPTOP-JBell:~$ fallocate -l 1K fileA
ubuntu@LAPTOP-JBell:~$ ls -lsh fileA
4.0K -rw-r--r-- 1 ubuntu ubuntu 1.0K Oct 21 23:01 fileA
ubuntu@LAPTOP-JBell:~$ wc --bytes fileA
1024 fileA
ubuntu@LAPTOP-JBell:~$ stat fileA
  File: fileA
  Size: 1024            Blocks: 8          IO Block: 4096   regular file
Device: 830h/2096d      Inode: 5109        Links: 1
Access: (0644/-rw-r--r--)  Uid: ( 1000/  ubuntu)   Gid: ( 1000/  ubuntu)
Access: 2025-10-21 23:01:13.439654623 -0400
Modify: 2025-10-21 23:01:13.439654623 -0400
Change: 2025-10-21 23:01:13.439654623 -0400
 Birth: 2025-10-21 23:01:13.439654623 -0400
```

```console
ubuntu@LAPTOP-JBell:~$ fallocate -l 100M fileB
ubuntu@LAPTOP-JBell:~$ ls -lsh fileB
100M -rw-r--r-- 1 ubuntu ubuntu 100M Oct 21 23:15 fileB
ubuntu@LAPTOP-JBell:~$ gzip -c fileB > fileB.gz
ubuntu@LAPTOP-JBell:~$ ls -lsh fileB.gz
100K -rw-r--r-- 1 ubuntu ubuntu 100K Oct 21 23:17 fileB.gz
```


