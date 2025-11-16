# Bash variables

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
ADJUST=1

echo NUMBER=$NUMBER
echo ADJUST=$ADJUST
global_variable $NUMBER $ADJUST
echo NUMBER=$NUMBER
local_variable $NUMBER $ADJUST
echo NUMBER=$NUMBER
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


