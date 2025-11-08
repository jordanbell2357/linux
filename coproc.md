# coproc

<https://mcturra2000.wordpress.com/2016/01/20/coprocesses-in-bash-using-dc-as-an-example/>

```bash
#!/usr/bin/env bash
#dc-coproc.sh

coproc mydc { dc; } # run process dc, calling it `mydc'

# define convenience functions for writing/reading to mydc
say () { echo "$1" >&"${mydc[1]}" ; } # echo 1st argument to mydc
get () { read res <&"${mydc[0]}" ; } # set var `res' is response

say "0" # initialise stack with 0

for v in 2 3 5 7
do
    say "$v + p"
    get
    echo "Val: $v, Running: $res" # produce output
done
say "q" # quit dc
```
