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

https://www.unicode.org/versions/latest/core-spec/chapter-23/#G20365

> There are 65 code points set aside in the Unicode Standard for compatibility with the C0 and C1 control codes defined in the ISO/IEC 2022 framework.
> The ranges of these code points are U+0000..U+001F, U+007F, and U+0080..U+009F, which correspond to the 8-bit controls 00₁₆ to 1F₁₆ (C0 controls),
> 7F₁₆ (*delete*), and 80₁₆ to 9F₁₆ (C1 controls), respectively.
> For example, the 8-bit legacy control code *character tabulation* (or *tab*) is the byte value 09₁₆; the Unicode Standard encodes the corresponding control code at U+0009.
>
> The Unicode Standard provides for the intact interchange of these code points, neither adding to nor subtracting from their semantics. The semantics of the control codes are generally determined by the application with which they are used. However, in the absence of specific application uses, they may be interpreted according to the control function semantics specified in ISO/IEC 6429:1992.
>
> In general, the use of control codes constitutes a higher-level protocol and is beyond the scope of the Unicode Standard. For example, the use of ISO/IEC 6429 control sequences
> for controlling bidirectional formatting would be a legitimate higher-level protocol layered on top of the plain text of the Unicode Standard.
> Higher-level protocols are not specified by the Unicode Standard; their existence cannot be assumed without a separate agreement between the parties interchanging such data.

