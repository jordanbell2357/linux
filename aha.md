# aha

<https://github.com/theZiz/aha>

<https://manpages.ubuntu.com/manpages//focal/man1/aha.1.html>

>   aha - Ansi HTML Adapter

<https://man7.org/linux/man-pages/man1/script.1.html>

<https://man7.org/linux/man-pages/man1/sar.1.html>

```console
ubuntu@LAPTOP-JBell:~$ script -q -c "sar -h -r 1 15" | aha -b > sar.html
```

```console
ubuntu@LAPTOP-JBell:~$ head -c 10G /dev/zero | pv -L 1G | tail > /dev/null
8.62GiB 0:00:17 [ 513MiB/s] [                               <=>                                                        ]
Killed
```

<https://jordanbell.info/assets/html/sar.html>
