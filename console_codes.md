# console_codes

https://wiki.osdev.org/Terminals

> When your OS is communicating over the serial like, it is very likely that on the other end there's a terminal. Either a real one, or a terminal emulator, like PuTTY or minicom.
> It is the terminal's duty to handle the keyboard, the key modifier keys (like Shift, Control, Alt), and send terminal key sequences.
> It is also the terminal's duty to interpret the received terminal codes (sometimes also called escape sequences) and visualize them properly.
> These sequences always start with the ASCII 27 (escape) character, "\033" in C literals, and terminated by a latin uppercase or lowercase letter or tilde ("~").
> In between there might be numeric parameters (0-9) separated by comma ("," and ";") but such arguments are always prefixed by "[".
> This two bytes start sequence "\033[" also called Control Sequence Introducer, or CSI.

```console
ubuntu@LAPTOP-JBell:~$ printf "\033[4B"; printf "CUD move the cursor down n=4 rows\n"




CUD move the cursor down n=4 rows
```

```console
ubuntu@LAPTOP-JBell:~$ printf "\033[6C"; printf "CUF move the cursor right n=6 columns\n"
      CUF move the cursor right n=6 columns
```

```console
ubuntu@LAPTOP-JBell:~$ printf "\033[4E"; printf "CNL move the cursor to the beginning of line n=4 down\n"




CNL move the cursor to the beginning of line n=4 down
```


```bash
printf "\033[2J"; printf "ED clear screen but preserve cursor position\n"
```


```console
ubuntu@LAPTOP-JBell:~$ printf "\x07BEL beeps\n"
BEL beeps
```
