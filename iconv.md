# iconv

https://man7.org/linux/man-pages/man1/iconv.1.html

```console
ubuntu@LAPTOP-JBell:~$ printf "\xa3\n"
�
ubuntu@LAPTOP-JBell:~$ printf "\xa3\n" | iconv -f ISO-8859-1 -t UTF-8
£
ubuntu@LAPTOP-JBell:~$ printf "\u00a3\n"
£
```


```console
ubuntu@LAPTOP-JBell:~$ printf "\xa9\n"
�
ubuntu@LAPTOP-JBell:~$ printf "\xa9\n" | iconv -f ISO-8859-1 -t UTF-8
©
ubuntu@LAPTOP-JBell:~$ printf "\u00a9\n"
©
```


```console
ubuntu@LAPTOP-JBell:~$ printf "\xe9\n"
�
ubuntu@LAPTOP-JBell:~$ printf "\xe9\n" | iconv -f ISO-8859-1 -t UTF-8
é
ubuntu@LAPTOP-JBell:~$ printf "\xe9" | iconv -f ISO-8859-1 -t UTF-8 | xxd
00000000: c3a9                                     ..
```


```console
ubuntu@LAPTOP-JBell:~$ printf "\xe3\n"
�
ubuntu@LAPTOP-JBell:~$ printf "\xe3\n" | iconv -f ISO-8859-1 -t UTF-8
ã
```


```console
ubuntu@LAPTOP-JBell:~$ printf "\xbc\n" | iconv -f ISO-8859-1 -t UTF-8
¼
ubuntu@LAPTOP-JBell:~$ printf "\xbd\n" | iconv -f ISO-8859-1 -t UTF-8
½
ubuntu@LAPTOP-JBell:~$ printf "\xbe\n" | iconv -f ISO-8859-1 -t UTF-8
¾
```
