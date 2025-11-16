# shuf

## -i, --input-range and -n, --head-count

Random integer between LO and HI:

```bash
LO=1
HI=15
shuf -i $LO-$HI -n 1
```

Manual page shuf:

```
-i, --input-range=LO-HI
treat each number LO through HI as an input line
```

```
 -n, --head-count=COUNT
output at most COUNT lines
```


## -e

```console
ubuntu@LAPTOP-JBell:~$ shuf -e dog cat cow
cow
dog
cat
```

Manual page shuf:

```
-e, --echo
treat each ARG as an input line
```

does the same as

```console
ubuntu@LAPTOP-JBell:~$ echo -e "dog\ncat\ncow" | shuf
cat
dog
cow
```

Manual page echo:

```
 -e     enable interpretation of backslash escapes
```
