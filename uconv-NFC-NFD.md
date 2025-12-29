# uconv NFC and NFD

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
> - - output data that may become input to unknown processes in NFC. 
> - - don't assume any normalization on input unless you control the data source.

https://aeb.win.tue.nl/linux/uc/nfc_vs_nfd.html

> In each equivalence class of canonically equivalent unicode sequences (all representing the same character), the Unicode Consortium singles out two representatives,
> Normalization Form C and Normalization Form D. Roughly speaking, NFC is the short form, fully composed, like U+1F85, and NFD is the long form, fully decomposed, in some well-defined order,
> like U+03B1 U+0314 U+0301 U+0345. (These are the two non-lossy normal forms. There are also lossy normalizations, not suitable for storage, but possibly suitable for search and comparison.)
> For full details, see [Unicode Normalization Forms](http://unicode.org/reports/tr15/).

https://www.unicode.org/reports/tr15/tr15-57.html#Canon_Compat_Equivalence

> The Unicode Standard defines two formal types of equivalence between characters: canonical equivalence and compatibility equivalence. Canonical equivalence is a fundamental equivalency between characters or sequences of characters which represent the same abstract character, and which when correctly displayed should always have the same visual appearance and behavior.

> Compatibility equivalence is a weaker type of equivalence between characters or sequences of characters which represent the same abstract character (or sequence of abstract characters), but which may have distinct visual appearances or behaviors.

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


## uconv

https://man7.org/linux/man-pages/man1/uconv.1.html

```console
ubuntu@LAPTOP-JBell:~$ printf "\u0065\u0301" | xxd
00000000: 65cc 81
```

```console
ubuntu@LAPTOP-JBell:~$ printf "\u00E9" | uconv -f utf8 -t utf8 -x nfd | xxd
00000000: 65cc 81
```

```console
ubuntu@LAPTOP-JBell:~$ printf "\u00E9" | uconv -f utf8 -t utf8 -x nfd | uniname -p
character  byte       UTF-32   encoded as     glyph   name
        0          0  000065   65             e      LATIN SMALL LETTER E
        1          1  000301   CC 81          ́      COMBINING ACUTE ACCENT
```

```console
ubuntu@LAPTOP-JBell:~$ printf "\u0065\u0301"
é
```

```console
ubuntu@LAPTOP-JBell:~$ printf "\u0065\u0301" | uconv -f utf8 -t utf8 -x nfc
é
```

```console
ubuntu@LAPTOP-JBell:~$ printf "\u0065\u0301" | uconv -f utf8 -t utf8 -x nfc | xxd
00000000: c3a9
```


```console
ubuntu@LAPTOP-JBell:~$ printf "\u0065\u0301" | uconv -f utf8 -t utf8 -x nfc | uniname -p
character  byte       UTF-32   encoded as     glyph   name
        0          0  0000E9   C3 A9          é      LATIN SMALL LETTER E WITH ACUTE
```


## Normalizing NFC and removing control characters 

Normalize UTF-8 data using Unicode NFC and remove all control characters.

\u0004 is EOT represented by ␄

```console
ubuntu@LAPTOP-JBell:~$ printf "\u0004\u0065\u0301"
é
```

```console
ubuntu@LAPTOP-JBell:~$ printf "\u0004\u0065\u0301" | xxd
00000000: 0465 cc81                                .e..
```

```console
ubuntu@LAPTOP-JBell:~$ printf "\u0004\u0065\u0301" | uconv -f utf8 -t utf8 -x '::nfc;' | xxd
00000000: 04c3 a9
```


```console
ubuntu@LAPTOP-JBell:~$ printf "\u0004\u0065\u0301" | uconv -f utf8 -t utf8 -x '[:Cc:] >;' | xxd
00000000: 65cc 81                                  e..
```


```console
ubuntu@LAPTOP-JBell:~$ printf "\u0004\u0065\u0301" | uconv -f utf8 -t utf8 -x '::nfc; [:Cc:] >;' | xxd
00000000: c3a9
```

## iconv

https://man7.org/linux/man-pages/man1/iconv.1.html

```console
ubuntu@LAPTOP-JBell:~$ printf "\u0004\u0065\u0301" | uconv -f utf8 -t utf8 -x '::nfc; [:Cc:] >;' | iconv -f UTF-8 -t ISO8859-1
�
```

```console
ubuntu@LAPTOP-JBell:~$ printf "\u0004\u0065\u0301" | uconv -f utf8 -t utf8 -x '::nfc; [:Cc:] >;' | iconv -f UTF-8 -t ISO8859-1 | xxd
00000000: e9
```

```console
ubuntu@LAPTOP-JBell:~$ printf "\xe9" | iconv -f ISO8859-1 -t UTF-8
é
ubuntu@LAPTOP-JBell:~$ printf "\xe9" | iconv -f ISO8859-1 -t UTF-8 | xxd
00000000: c3a9                                     ..
```


