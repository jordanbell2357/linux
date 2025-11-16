# Bash variables

<https://wiki.ghpc.au.dk/bash.html>

```bash
#!/usr/bin/env bash
# hello.sh
echo 'Hello World'
```

```console
ubuntu@LAPTOP-JBell:~$ vi hello.sh
ubuntu@LAPTOP-JBell:~$ chmod +x hello.sh
ubuntu@LAPTOP-JBell:~$ ./hello.sh
Hello World
```


```bash
#!/usr/bin/env bash
# variables.sh

global_variable() {
        NUMBER=$(($1+$2));
        echo ${FUNCNAME[0]} NUMBER=$NUMBER;
}

local_variable() {
        local NUMBER=$(($1+$2));
        echo ${FUNCNAME[0]} NUMBER=$NUMBER;
}

NUMBER=$1
RANDOM_NOISE=$(shuf -i 10-15 -n 1)

echo NUMBER=$NUMBER
echo RANDOM_NOISE=$RANDOM_NOISE
global_variable $NUMBER $RANDOM_NOISE
echo NUMBER=$NUMBER
local_variable $NUMBER $RANDOM_NOISE
echo NUMBER=$NUMBER
```

```console
ubuntu@LAPTOP-JBell:~$ ./variables.sh 60
NUMBER=60
RANDOM_NOISE=11
global_variable NUMBER=71
NUMBER=71
local_variable NUMBER=82
NUMBER=71
```


> A variable can also be set for a single program in the current scope/shell using the one-line syntax:
>
> `VARIABLE1="value1" VARIABLE2="value2" run_program`

```console
ubuntu@LAPTOP-JBell:~$ date
Sat Nov 15 20:15:16 EST 2025
ubuntu@LAPTOP-JBell:~$ TZ=UTC date
Sun Nov 16 01:15:12 UTC 2025
```


