# Here Documents

Brian W. Kernighan and Rob Pike, The Unix Programming Environment, Prentice-Hall, 1984. Section 3.7, p. 94:

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
