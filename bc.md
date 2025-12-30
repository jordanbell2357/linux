# bc

https://www.gnu.org/software/bc/manual/html_mono/bc.html

> There are four special variables, *scale*, *ibase*, *obase*, and *last*.
> *scale* defines how some operations use digits after the decimal point.
> The default value of *scale* is 0. *ibase* and *obase* define the conversion base for input and output numbers.
> The default for both input and output is base 10. *last* (an extension) is a variable that has the value of the last printed number.
> These will be discussed in further detail where appropriate. All of these variables may have values assigned to them as well as used in expressions.

`-l, --mathlib`:

> If bc is invoked with the `-l` option, a math library is preloaded and the default `scale` is set to 20.


```console
ubuntu@laptop:~$ echo 'scale' | bc
0
ubuntu@laptop:~$ echo '100 / 37' | bc
2
```

```console
ubuntu@laptop:~$ echo 'scale' | bc -l
20
```

We can specify the scale:

```console
ubuntu@laptop:~$ echo 'scale=5; scale' | bc
5
ubuntu@laptop:~$ echo 'scale=5; 1 / 0.37' | bc
2.70270
```

https://www.linuxjournal.com/content/fancy-tricks-changing-numeric-base

```console
ubuntu@laptop:~$ echo 'obase=16; 13' | bc
D
```

This is an occasion to repeat an integer (42) a given number of times (3).

We want to accomplish the following while only writing 42 once:

```console
ubuntu@laptop:~$ printf "decimal: %d\nhex: %x\noctal: %o\n" 42 42 42
decimal: 42
hex: 2a
octal: 52
```

Using yes and head.

```console
ubuntu@laptop:~$ yes 42 | head -n 3 | xargs printf "decimal: %d\nhex: %x\noctal: %o\n"
decimal: 42
hex: 2a
octal: 52
```


