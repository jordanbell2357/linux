# teseq

https://www.gnu.org/software/teseq/

```console
ubuntu@LAPTOP-JBell:~$ printf '\033[1mHi\033[m there, world' > out; sleep 1; printf '\b\b\b\b\bearth\n' >> out
ubuntu@LAPTOP-JBell:~$ cat out
Hi there, earth
ubuntu@LAPTOP-JBell:~$ cat -A out
^[[1mHi^[[m there, world^H^H^H^H^Hearth$
ubuntu@LAPTOP-JBell:~$ teseq out
: Esc [ 1 m
& SGR: SELECT GRAPHIC RENDITION
" Set bold text.
|Hi|
: Esc [ m
& SGR: SELECT GRAPHIC RENDITION
" Clear graphic rendition to defaults.
| there, world|
. BS/^H BS/^H BS/^H BS/^H BS/^H
|earth|.
```

> The `teseq` command can be instructed to recognize, but not output, escapes encountered in the input. This is useful for stripping out the formatting strings that are invisible on display,
> but which get in the way during editing, or make the content inappropriate for inclusion in documentation, etc.
>
> To sanitize a typescript file or other text file containing control sequences, try the following command:
>
> `$ teseq -EDLC your-file.txt | reseq - - | col -b > new-file.txt`
>
> The `-EDLC` options tell `teseq` not to output recognized escape sequences or identify them, and otherwise to abbreviate its output. Then,
> `reseq` takes the output from `teseq` and turns it back into raw text (minus the now elided escape sequences).
> Finally, `col -b` (a fairly standard Unix tool) interprets common control characters such as backspaces and carriage returns, resolving them into a text file that displays the same,
> but doesn't contain those controls.

```console
ubuntu@LAPTOP-JBell:~$ teseq -EDLC out | reseq - - | col -b > cleaned
```

```console
ubuntu@LAPTOP-JBell:~$ cat cleaned
Hi there, earth
```

```console
ubuntu@LAPTOP-JBell:~$ cat -A cleaned
Hi there, earth$
```

```console
ubuntu@LAPTOP-JBell:~$ teseq cleaned
|Hi there, earth|.
```


