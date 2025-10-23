# pv

> pv - monitor and manage the progress of data through a pipe

<https://www.ivarch.com/programs/quickref/pv.shtml>


```console
ubuntu@LAPTOP-JBell:~$ echo -n hello | wc -c
5
ubuntu@LAPTOP-JBell:~$ echo hello | wc -c
6
ubuntu@LAPTOP-JBell:~$ timeout 1 bash -c "yes hello | pv -q -L 6"
hello
ubuntu@LAPTOP-JBell:~$ timeout 1 bash -c "yes hello | pv -q -L 3"
hel
ubuntu@LAPTOP-JBell:~$ timeout 8 bash -c "yes hello | pv -q -L 6"
hello
hello
hello
hello
hello
hello
hello
hello
```
