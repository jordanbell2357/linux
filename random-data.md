# Random data generation and formatting

## dd, xxd

```bash
dd if=/dev/urandom count=1 bs=32 status=none | xxd -c 8 -p
```

```
84681e94eab32045
ea7cd36ab119cac9
dd97ee9cf1d9de9d
c80c707f974211ea
```

## dd, base64

<https://ss64.com/bash/base64.html>

```bash
dd if=/dev/urandom count=1 bs=32 status=none | base64 -w 16
```

```console
lhs4Q1hA+KxKrkxR
/9xlvsZcmE4lWrr3
WGPJp5tM5xg=
```



## dd, tr, fold, sed

```bash
dd if=/dev/random bs=1024 count=1 status=none |
 tr -cd 'A-Za-z0-9' |
 dd bs=128 count=1 status=none conv=unblock |
 fold -w 16 |
 sed -r '$ s/(.*)/&\n/'
```

```
3cTFOPN8YspO7i2n
1K7rf9MZJ2IWjMCC
Vsu4DVxg6VDxJc1f
qwZvGSPQg6GW3uMc
tTwmSYyRlpoUWCEp
MNWB4XneWi3rBRa7
4fVLIq8PGnmEvYKp
MFefPyRvbqtQsPqS
```

## dd, tr, xargs, printf

```bash
dd if=/dev/random bs=1024 count=1 status=none |
 tr -cd 'A-Za-z0-9' |
 dd bs=128 count=1 status=none conv=unblock |
 fold -w 16 |
 xargs printf "%s\n"
```

```
ohNxbQwdTbwlCWMz
gE4JAAqV5XLcyjlP
XWNWKbczmFmJ3QHe
n4JviEuWKvagAYFS
UTyURz49bj4hLjb3
UYkT0N2GFxBepBuh
jdaLxlXPqI8lQZD8
eOk7w2idQ8Nqi2Wo
```

## /usr/share/dict/words

<https://refspecs.linuxfoundation.org/FHS_3.0/fhs/ch04s11.html#usrsharedictWordLists>

```bash
shuf -n 10 /usr/share/dict/words
```

```
loopier
daffy
flout
Peruvian's
Reid's
readjust
clicks
added
autoworkers
skateboard's
```

## Timezones

```console
ubuntu@LAPTOP-JBell:~$ timedatectl list-timezones | grep America | shuf -n 10
America/Matamoros
America/St_Thomas
America/Thunder_Bay
America/Atka
America/Grenada
America/Noronha
America/Kralendijk
America/Merida
America/Boise
America/Guyana
```
