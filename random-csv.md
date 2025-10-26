# Random CSV


## Creating and chunking random text

```console
ubuntu@LAPTOP-JBell:~$ dd if=/dev/random bs=1024 count=1 status=none |
tr -cd 'A-Za-z0-9' |
dd bs=128 count=1 status=none conv=unblock |
fold -w 16 |
sed -r '$ s/(.*)/&\n/'
3cTFOPN8YspO7i2n
1K7rf9MZJ2IWjMCC
Vsu4DVxg6VDxJc1f
qwZvGSPQg6GW3uMc
tTwmSYyRlpoUWCEp
MNWB4XneWi3rBRa7
4fVLIq8PGnmEvYKp
MFefPyRvbqtQsPqS
```

```console
ubuntu@LAPTOP-JBell:~$ dd if=/dev/random bs=1024 count=1 status=none | tr -cd 'A-Za-z0-9' | dd bs=128 count=1 status=none conv=unblock | fold -w 16 | xargs printf "%s\n"
ohNxbQwdTbwlCWMz
gE4JAAqV5XLcyjlP
XWNWKbczmFmJ3QHe
n4JviEuWKvagAYFS
UTyURz49bj4hLjb3
UYkT0N2GFxBepBuh
jdaLxlXPqI8lQZD8
eOk7w2idQ8Nqi2Wo
```


## UUID

<https://linux.die.net/man/1/uuid>




## /usr/share/dict/words

<https://refspecs.linuxfoundation.org/FHS_3.0/fhs/ch04s11.html#usrsharedictWordLists>
