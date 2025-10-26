# Random CSV


## Random text

```console
ubuntu@LAPTOP-JBell:~$ dd if=/dev/random bs=1024 count=1 status=none | tr -cd 'A-Za-z0-9' | dd bs=128 count=1 status=none conv=unblock | fold -w 16 | xargs printf "%s\n" | sed 's/.*$/&\n/g'
QT6biXAxnmF7JXYV
oV7jzdaJoplnajj6
J0PTpgduLyuOWjUH
Xlv3h4pFqsPBUuCL
41Yts4dvszUtLO7m
xSTtsPsRUxEGugqF
Ks2RUpsIwy1XDP1W
T5EvCDlX6CtHulqj
```


## UUID

<https://linux.die.net/man/1/uuid>




## /usr/share/dict/words

<https://refspecs.linuxfoundation.org/FHS_3.0/fhs/ch04s11.html#usrsharedictWordLists>
