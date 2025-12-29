# Bash read

## read

https://pubs.opengroup.org/onlinepubs/7908799/xcu/read.html

https://www.gnu.org/software/bash/manual/bash.html#Bash-Builtins

https://www.baeldung.com/linux/read-command

https://www.spsanderson.com/steveondata/posts/2025-03-21/

https://ss64.com/bash/read.html

> One line is read from the standard input, and the first word is assigned to the first `name`, the second word to the second `name`, and so on,
> with leftover words and their intervening separators assigned to the last `name`.
>
> The read command modifies each line read; by default it removes all leading and trailing whitespace characters (spaces and tabs, or any whitespace characters present in IFS).
> If that is not desired, the IFS variable can be cleared with IFS=

If there are fewer words read from the standard input than names, the remaining names are assigned empty values.
The characters in the value of the IFS variable are used to split the line into words.

```console
ubuntu@LAPTOP-JBell:~$ read
one two three four five six tab seven
ubuntu@LAPTOP-JBell:~$ echo $REPLY
one two three four five six tab seven
```

```console
ubuntu@LAPTOP-JBell:~$ read -a names
first_word second-word third_word_followed_by_tab       last_word
ubuntu@LAPTOP-JBell:~$ echo ${names[0]}
first_word
ubuntu@LAPTOP-JBell:~$ echo ${names[-1]}
last_word
ubuntu@LAPTOP-JBell:~$ echo ${names[@]}
first_word second-word third_word_followed_by_tab last_word
```

## Internal Field Separator (IFS)

https://tldp.org/LDP/abs/html/special-chars.html

> Definition: A field is a discrete chunk of data expressed as a string of consecutive characters. Separating each field from adjacent fields is either whitespace or some other designated character
> (often determined by the $IFS). In some contexts, a field may be called a record.

```console
ubuntu@LAPTOP-JBell:~$ IFS=$(printf '\x09') read name1 name2
a       b       c       d
ubuntu@LAPTOP-JBell:~$ echo $name1
a
ubuntu@LAPTOP-JBell:~$ echo $name2
b c d
```

https://www.gnu.org/software/bash/manual/bash.html#Word-Splitting-1

> The shell scans the results of parameter expansion, command substitution, and arithmetic expansion that did not occur within double quotes for word splitting. Words that were not expanded are not split.
>
> The shell treats each character of $IFS as a delimiter, and splits the results of the other expansions into fields using these characters as field terminators.
>
> An IFS whitespace character is whitespace as defined above (see Definitions) that appears in the value of IFS. Space, tab, and newline are always considered IFS whitespace, even if they don’t appear in the
> locale’s space category.
>
> If IFS is unset, word splitting behaves as if its value were <space><tab><newline>, and treats these characters as IFS whitespace.
> If the value of IFS is null, no word splitting occurs, but implicit null arguments (see below) are still removed.

Word splitting begins by removing sequences of IFS whitespace characters from the beginning and end of the results of the previous expansions, then splits the remaining words.


```console
ubuntu@LAPTOP-JBell:~$ read
dog cat NL
ubuntu@LAPTOP-JBell:~$ echo $?
0
ubuntu@LAPTOP-JBell:~$ echo $REPLY
dog cat NL
```

We enter the control code for EOT by <kbd>Ctrl</kbd> + <kbd>d</kbd>, in caret notation ^d. This has ASCII code x04:

```console
ubuntu@LAPTOP-JBell:~$ printf "\x04" |  uniname -p
character  byte       UTF-32   encoded as     glyph   name
        0          0  000004   04                     END OF TRANSMISSION
```

Using this control code,

```console
ubuntu@LAPTOP-JBell:~$ read
dog cat EOF
ubuntu@LAPTOP-JBell:~$ echo $?
1
ubuntu@LAPTOP-JBell:~$ echo $REPLY
dog cat EOT
ubuntu@LAPTOP-JBell:~$ echo $REPLY | xxd
00000000: 646f 6720 6361 7420 454f 460a            dog cat EOT.
```




