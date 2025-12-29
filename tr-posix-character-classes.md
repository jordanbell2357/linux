# tr POSIX character classes

https://www.gnu.org/software/coreutils/manual/html_node/Character-arrays.html

https://pubs.opengroup.org/onlinepubs/009696699/basedefs/xbd_chap09.html

https://man7.org/linux/man-pages/man1/tr.1.html

```console
ubuntu@LAPTOP-JBell:~$ printf "\u0065\n"
e
ubuntu@LAPTOP-JBell:~$ printf "\u0065\n" | tr -d '[:alnum:]'

ubuntu@LAPTOP-JBell:~$ printf "\u011B\n"
ě
ubuntu@LAPTOP-JBell:~$ printf "\u011B\n" | tr -d '[:alnum:]'
ě
```


```console
ubuntu@LAPTOP-JBell:~$ printf "\u000C" | uniname -p
character  byte       UTF-32   encoded as     glyph   name
        0          0  00000C   0C                     FORM FEED (FF)
```


```console
ubuntu@LAPTOP-JBell:~$ printf "Hi\u000C" | tr -d '[:cntrl:]' | wc -c
2
```

