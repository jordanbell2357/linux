# ulimit

<https://ss64.com/bash/ulimit.html>

<https://tldp.org/LDP/solrhe/Securing-Optimizing-Linux-RH-Edition-v1.3/x4733.html>

```bash
vmstat -S M
```

```console
procs -----------memory---------- ---swap-- -----io---- -system-- -------cpu-------
 r  b   swpd   free   buff  cache   si   so    bi    bo   in   cs us sy id wa st gu
 1  0      0   7264      4    147    0    0    22    44  282    1  0  0 100  0  0  0
```

```bash
dd if=/dev/zero bs=100M count=100 | tail > /dev/null; echo $?
```

This has exit code 137:

```console
Killed
137
```

`ulimit -v` limits the size of the virtual memory to a given number of 1024 byte increments.

```bash
(ulimit -v 500000; dd if=/dev/zero bs=100M count=100 | tail > /dev/null; echo $?)
```

This has exit code 1:

```console
tail: memory exhausted
1
```

While if we make the dd block size larger than the virtual memory limit, we get the following

```bash
(ulimit -v 500000; dd if=/dev/zero bs=1G count=10 | tail > /dev/null; echo $?)
```

this has exit code 0:

```console
dd: memory exhausted by input buffer of size 1073741824 bytes (1.0 GiB)
0
```


