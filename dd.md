# dd

<https://blog.kubesimplify.com/the-complete-guide-to-the-dd-command-in-linux>

<https://ss64.com/bash/dd.html>

## conv

```console
ubuntu@LAPTOP-JBell:~$ echo hello > hello.txt
ubuntu@LAPTOP-JBell:~$ dd if=hello.txt status=none
hello
ubuntu@LAPTOP-JBell:~$ dd if=hello.txt status=none conv=ucase
HELLO
```

## iflag

<https://www.pixelbeat.org/docs/coreutils-gotchas.html>

> dd iflag=fullblock is usually what you want because when reading from a fifo/pipe you often get a short read, which means you get too little data if you specify "count", or too much data if you specify "sync". For example:


We replicate this with a Bash for loop:

```console
ubuntu@LAPTOP-JBell:~$ for i in {1..5}; do dd status=none bs=1 count=512 if=/dev/zero | dd status=none count=1 bs=512 | wc -c; done
82
176
73
122
17
```

We also do this multiple times using GNU parallel: [^1]
[^1]: <http://www.gnu.org/software/parallel/parallel_tutorial.html>

```console
ubuntu@LAPTOP-JBell:~$ parallel -n0 'dd status=none bs=1 count=512 if=/dev/zero | dd status=none count=1 bs=512 | wc -c' ::: {1..5}
16
409
128
390
496
```

On the second invocation of dd, we use `iflag=fullblock`:

```console
ubuntu@LAPTOP-JBell:~$ for i in {1..5}; do dd status=none bs=1 count=512 if=/dev/zero | dd status=none iflag=fullblock count=1 bs=512 | wc -c; done
512
512
512
512
512
```

## Sparse files

10M file:

```console
ubuntu@LAPTOP-JBell:~$ dd if=/dev/zero of=spacer.img bs=1 count=0 seek=10M
0+0 records in
0+0 records out
0 bytes copied, 2.4013e-05 s, 0.0 kB/s
ubuntu@LAPTOP-JBell:~$ du -h spacer.img
0       spacer.img
ubuntu@LAPTOP-JBell:~$ ls -lsh spacer.img
0 -rw-r--r-- 1 ubuntu ubuntu 10M Oct 21 01:56 spacer.img
ubuntu@LAPTOP-JBell:~$ wc --bytes spacer.img
10485760 spacer.img
ubuntu@LAPTOP-JBell:~$ stat spacer.img
  File: spacer.img
  Size: 10485760        Blocks: 0          IO Block: 4096   regular file
Device: 830h/2096d      Inode: 125455      Links: 1
Access: (0644/-rw-r--r--)  Uid: ( 1000/  ubuntu)   Gid: ( 1000/  ubuntu)
Access: 2025-10-21 01:57:09.953531490 -0400
Modify: 2025-10-21 01:56:48.465535955 -0400
Change: 2025-10-21 01:56:48.465535955 -0400
 Birth: 2025-10-21 01:09:37.350161788 -0400
```

<https://askubuntu.com/a/506962/2362743>

100MB file:

```console
ubuntu@LAPTOP-JBell:~$ dd if=/dev/zero of=zeros.img count=1 bs=1 seek=$((100 * 1024 * 1024 - 1))
1+0 records in
1+0 records out
1 byte copied, 3.5948e-05 s, 27.8 kB/s
ubuntu@LAPTOP-JBell:~$ du -h zeros.img
4.0K    zeros.img
ubuntu@LAPTOP-JBell:~$ ls -lsh zeros.img
8.0K -rw-r--r-- 1 ubuntu ubuntu 1.0G Oct 21 02:03 zeros.img
ubuntu@LAPTOP-JBell:~$ wc --bytes zeros.img
104857600 zeros.img
ubuntu@LAPTOP-JBell:~$ stat zeros.img
  File: zeros.img
  Size: 104857600       Blocks: 8          IO Block: 4096   regular file
Device: 830h/2096d      Inode: 5109        Links: 1
Access: (0644/-rw-r--r--)  Uid: ( 1000/  ubuntu)   Gid: ( 1000/  ubuntu)
Access: 2025-10-21 01:59:25.353496131 -0400
Modify: 2025-10-21 01:59:11.681500836 -0400
Change: 2025-10-21 01:59:11.681500836 -0400
 Birth: 2025-10-21 00:26:21.550743635 -0400
```

```console
ubuntu@LAPTOP-JBell:~$ dd if=/dev/zero count=64 bs=10M | gzip -c > zero.img.gz
64+0 records in
64+0 records out
671088640 bytes (671 MB, 640 MiB) copied, 2.78351 s, 241 MB/s
ubuntu@LAPTOP-JBell:~$ du -h zero.img.gz
640K    zero.img.gz
ubuntu@LAPTOP-JBell:~$ ls -lsh zero.img.gz
640K -rw-r--r-- 1 ubuntu ubuntu 637K Oct 21 03:32 zero.img.gz
ubuntu@LAPTOP-JBell:~$ stat zero.img.gz
  File: zero.img.gz
  Size: 651302          Blocks: 1280       IO Block: 4096   regular file
Device: 830h/2096d      Inode: 5237        Links: 1
Access: (0644/-rw-r--r--)  Uid: ( 1000/  ubuntu)   Gid: ( 1000/  ubuntu)
Access: 2025-10-21 03:32:03.152583372 -0400
Modify: 2025-10-21 03:32:19.165222895 -0400
Change: 2025-10-21 03:32:19.165222895 -0400
 Birth: 2025-10-21 03:32:03.152583372 -0400
ubuntu@LAPTOP-JBell:~$ wc --bytes zero.img.gz
651302 zero.img.gz
```

