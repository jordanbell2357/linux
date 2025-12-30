# Bash Here Documents

Brian W. Kernighan and Rob Pike, The Unix Programming Environment, Prentice-Hall, 1984. Section 3.7, p. 94:

<https://archive.org/details/UnixProgrammingEnviornment/page/n105/mode/1up>

> The shell jargon for this construction is a here document; it means that the input is right here instead of in a file somewhere.
> The `<<` signals the construction; the word that follows (`End` in our example) is used to delimit the input, which is taken to be
> everything up to an occurrence of that word on a line by itself. The shell substitutes for `$`, `` `...` ``, and `\` in a here document,
> unless some part of the word is quoted with quotes or a backslash; in that case, the whole document is taken literally.

https://tldp.org/LDP/abs/html/here-docs.html

```console
ubuntu@LAPTOP-JBell:~$ cat > output_file <<EOF
A
$LANGUAGE
`echo "obase=16; 11" | bc`
EOF
ubuntu@LAPTOP-JBell:~$ cat output_file
A
C
B
```

<https://ss64.com/bash/syntax-here.html>



<https://www.grymoire.com/Unix/Quote.html#toc-uh-10>

> There is another type of quote the shells support. There are called **Here is** documents. There are used when you need to read something from standard input, but you don't want to create a file to provide that input. You can use this as another way to have dynamic variables inside a shell script. There are also used to create files in a shell script. A <tt>HERE IS</tt> document can be created by the "<<" character, followed by a special word:

```console
ubuntu@LAPTOP-JBell:~$ sort >file <<EndOfSort
> zygote
> abacus
> EndOfSort
ubuntu@LAPTOP-JBell:~$ cat file
abacus
zygote
```
