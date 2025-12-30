# Bash variables

## Assignment

We make the following file `hello.sh`

```bash
#!/usr/bin/env bash
# hello.sh
echo 'Hello World'
```

Then

```console
ubuntu@LAPTOP-JBell:~$ chmod +x hello.sh
ubuntu@LAPTOP-JBell:~$ ./hello.sh
Hello World
```

https://ss64.com/bash/syntax-variables.html

> A variable can also be set for a single program in the current scope/shell using the one-line syntax:
>
> `VARIABLE1="value1" VARIABLE2="value2" run_program`

```console
ubuntu@LAPTOP-JBell:~$ date
Sat Nov 15 20:15:16 EST 2025
ubuntu@LAPTOP-JBell:~$ TZ=UTC date
Sun Nov 16 01:15:12 UTC 2025
ubuntu@LAPTOP-JBell:~$ date
Sat Nov 15 20:15:16 EST 2025
```

## Local variables

https://tldp.org/LDP/abs/html/localvar.html

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
ADJUST=1

echo NUMBER=$NUMBER
echo ADJUST=$ADJUST
global_variable $NUMBER $ADJUST
echo NUMBER=$NUMBER
local_variable $NUMBER $ADJUST
echo NUMBER=$NUMBER
```

## env

https://ss64.com/bash/env.html


## export

https://ss64.com/bash/export.html


## declare

https://ss64.com/bash/declare.html
