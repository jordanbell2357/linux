# fallocate, truncate and gzip

## fallocate

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
ubuntu@LAPTOP-JBell:~$ wc --bytes fileB
104857600 fileB
ubuntu@LAPTOP-JBell:~$ stat fileB
  File: fileB
  Size: 104857600       Blocks: 204800     IO Block: 4096   regular file
Device: 830h/2096d      Inode: 5109        Links: 1
Access: (0644/-rw-r--r--)  Uid: ( 1000/  ubuntu)   Gid: ( 1000/  ubuntu)
Access: 2025-10-21 23:15:34.830853202 -0400
Modify: 2025-10-21 23:15:27.934852893 -0400
Change: 2025-10-21 23:15:27.934852893 -0400
 Birth: 2025-10-21 23:15:27.934852893 -0400
ubuntu@LAPTOP-JBell:~$ gzip -c fileB > fileB.gz
ubuntu@LAPTOP-JBell:~$ ls -lsh fileB.gz
100K -rw-r--r-- 1 ubuntu ubuntu 100K Oct 21 23:17 fileB.gz
```

## truncate

<https://man7.org/linux/man-pages/man1/truncate.1.html>

```console
ubuntu@LAPTOP-JBell:~$ truncate -s 100M fileC
ubuntu@LAPTOP-JBell:~$ ls -lsh fileC
0 -rw-r--r-- 1 ubuntu ubuntu 100M Oct 21 23:23 fileC
ubuntu@LAPTOP-JBell:~$ wc --bytes fileC
104857600 fileC
ubuntu@LAPTOP-JBell:~$ stat fileC
  File: fileC
  Size: 104857600       Blocks: 0          IO Block: 4096   regular file
Device: 830h/2096d      Inode: 7088        Links: 1
Access: (0644/-rw-r--r--)  Uid: ( 1000/  ubuntu)   Gid: ( 1000/  ubuntu)
Access: 2025-10-21 23:24:14.482738216 -0400
Modify: 2025-10-21 23:23:59.222742059 -0400
Change: 2025-10-21 23:23:59.222742059 -0400
 Birth: 2025-10-21 23:23:59.222742059 -0400
ubuntu@LAPTOP-JBell:~$ gzip -c fileC > fileC.gz
ubuntu@LAPTOP-JBell:~$ ls -lsh fileC.gz
100K -rw-r--r-- 1 ubuntu ubuntu 100K Oct 21 23:25 fileC.gz
ubuntu@LAPTOP-JBell:~$ wc --bytes fileC.gz
101797 fileC.gz
```
