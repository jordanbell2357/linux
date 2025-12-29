# uconv NFC and NFD

https://man7.org/linux/man-pages/man1/uconv.1.html

```console
ubuntu@LAPTOP-JBell:~$ printf "\x09" | uconv -f utf-8 -x any-name
\N{<control-0009>}
```

https://scripts.sil.org/nfc_vs_nfd.html

> **Axiom**
>
> As far as Unicode text is concerned, fully decomposed (NFD), fully composed (NFC) and any other canonically equivalent representation are all interchangeable — all are equally correct representations of
> the Unicode text in question, and no one representation is considered preferred by the Unicode Standard.

> **Corollary**
>
> Text processes are free to change data at will to any canonically equivalent representation.
>
> **Corollary**
>
> It is inappropriate to speak of standardizing on one particular representation such as NFD or NFC except in the context of a specific text process or data interchange format.

> Question: Given all of the above, are there any specific recommendations?
>
> Answer: A colleague suggests the following:
>
> - programmers:
> -- output data that may become input to unknown processes in NFC.
> -- don't assume any normalization on input unless you control the data source.

## NFC

NFC: `é`

```console
ubuntu@LAPTOP-JBell:~$ printf "\u00e9\n"
é
```

```console
ubuntu@LAPTOP-JBell:~$ printf "\u00e9" | uniname -p
character  byte       UTF-32   encoded as     glyph   name
        0          0  0000E9   C3 A9          é      LATIN SMALL LETTER E WITH ACUTE
```



```console
ubuntu@LAPTOP-JBell:~$ printf é | uniname -p
character  byte       UTF-32   encoded as     glyph   name
        0          0  0000E9   C3 A9          é      LATIN SMALL LETTER E WITH ACUTE
```


## NFD

NFD: `é`

```console
ubuntu@LAPTOP-JBell:~$ printf "\u0065\u0301\n"
é
```

```console
ubuntu@LAPTOP-JBell:~$ printf "\u0065\u0301" | uniname -p
character  byte       UTF-32   encoded as     glyph   name
        0          0  000065   65             e      LATIN SMALL LETTER E
        1          1  000301   CC 81          ́      COMBINING ACUTE ACCENT
```

```console
ubuntu@LAPTOP-JBell:~$ printf é | uniname -p
character  byte       UTF-32   encoded as     glyph   name
        0          0  000065   65             e      LATIN SMALL LETTER E
        1          1  000301   CC 81          ́      COMBINING ACUTE ACCENT
```



