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
        MINUTES=$(($1+$2));
        echo ${FUNCNAME[0]} MINUTES=$MINUTES;
}

local_variable() {
        local MINUTES=$(($1+$2));
        echo ${FUNCNAME[0]} MINUTES=$MINUTES;
}

add_minutes() {
        local MINUTES=$(($1+$2));
        echo ${FUNCNAME[0]} $(date -d "$MINUTES minutes")
}

MINUTES=$1
RANDOM_NOISE=$(shuf -i 10-15 -n 1)

echo $0 MINUTES=$MINUTES
echo $0 RANDOM_NOISE=$RANDOM_NOISE
global_variable $MINUTES $RANDOM_NOISE
echo $0 MINUTES=$MINUTES
echo $0 RANDOM_NOISE=$RANDOM_NOISE
local_variable $MINUTES $RANDOM_NOISE
echo $0 MINUTES=$MINUTES
echo $0 RANDOM_NOISE=$RANDOM_NOISE
add_minutes $MINUTES $RANDOM_NOISE
echo $0 MINUTES=$MINUTES
echo $0 RANDOM_NOISE=$RANDOM_NOISE
```

```console
ubuntu@LAPTOP-JBell:~$ ./variables.sh 60
./variables.sh MINUTES=60
./variables.sh RANDOM_NOISE=15
global_variable MINUTES=75
./variables.sh MINUTES=75
./variables.sh RANDOM_NOISE=15
local_variable MINUTES=90
./variables.sh MINUTES=75
./variables.sh RANDOM_NOISE=15
add_minutes Sat Nov 15 21:01:27 EST 2025
./variables.sh MINUTES=75
./variables.sh RANDOM_NOISE=15
```

