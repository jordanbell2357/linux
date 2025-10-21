# xxd

<https://ss64.com/bash/xxd.html>

```console
ubuntu@LAPTOP-JBell:~$ echo hello > hello.txt
ubuntu@LAPTOP-JBell:~$ dd if=hello.txt status=none
hello
ubuntu@LAPTOP-JBell:~$ xxd hello.txt
00000000: 6865 6c6c 6f0a                           hello.
ubuntu@LAPTOP-JBell:~$ xxd -p hello.txt
68656c6c6f0a
ubuntu@LAPTOP-JBell:~$ dd if=/dev/urandom count=1 bs=1 status=none | xxd -p
8d
ubuntu@LAPTOP-JBell:~$ dd if=/dev/urandom count=1 bs=1 status=none | xxd -l1 -p
ubuntu@LAPTOP-JBell:~$ dd if=/dev/zero count=1 bs=1 status=none | xxd -p
00
```
