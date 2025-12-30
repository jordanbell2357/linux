# uconv

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
ubuntu@laptop:~$ printf "\u00e9\n"
é
```

```console
ubuntu@laptop:~$ printf "\u00e9" | uniname -p
character  byte       UTF-32   encoded as     glyph   name
        0          0  0000E9   C3 A9          é      LATIN SMALL LETTER E WITH ACUTE
```



```console
ubuntu@laptop:~$ printf é | uniname -p
character  byte       UTF-32   encoded as     glyph   name
        0          0  0000E9   C3 A9          é      LATIN SMALL LETTER E WITH ACUTE
```


## NFD

NFD: `é`

```console
ubuntu@laptop:~$ printf "\u0065\u0301\n"
é
```

```console
ubuntu@laptop:~$ printf "\u0065\u0301" | uniname -p
character  byte       UTF-32   encoded as     glyph   name
        0          0  000065   65             e      LATIN SMALL LETTER E
        1          1  000301   CC 81          ́      COMBINING ACUTE ACCENT
```

```console
ubuntu@laptop:~$ printf é | uniname -p
character  byte       UTF-32   encoded as     glyph   name
        0          0  000065   65             e      LATIN SMALL LETTER E
        1          1  000301   CC 81          ́      COMBINING ACUTE ACCENT
```


## uconv

https://man7.org/linux/man-pages/man1/uconv.1.html

```console
ubuntu@laptop:~$ printf "\u0065\u0301" | xxd
00000000: 65cc 81
```

```console
ubuntu@laptop:~$ printf "\u00E9" | uconv -f utf8 -t utf8 -x nfd | xxd
00000000: 65cc 81
```

```console
ubuntu@laptop:~$ printf "\u00E9" | uconv -f utf8 -t utf8 -x nfd | uniname -p
character  byte       UTF-32   encoded as     glyph   name
        0          0  000065   65             e      LATIN SMALL LETTER E
        1          1  000301   CC 81          ́      COMBINING ACUTE ACCENT
```

```console
ubuntu@laptop:~$ printf "\u0065\u0301"
é
```

```console
ubuntu@laptop:~$ printf "\u0065\u0301" | uconv -f utf8 -t utf8 -x nfc
é
```

```console
ubuntu@laptop:~$ printf "\u0065\u0301" | uconv -f utf8 -t utf8 -x nfc | xxd
00000000: c3a9
```


```console
ubuntu@laptop:~$ printf "\u0065\u0301" | uconv -f utf8 -t utf8 -x nfc | uniname -p
character  byte       UTF-32   encoded as     glyph   name
        0          0  0000E9   C3 A9          é      LATIN SMALL LETTER E WITH ACUTE
```


## Unicode General_Category property

https://www.unicode.org/versions/Unicode17.0.0/core-spec/chapter-4/#G132145

> **Aliases.** Character properties and their values are given formal aliases to make it easier to refer to them consistently in specifications and in implementations, such as regular expressions, which may use them. These aliases are listed exhaustively in the Unicode Character Database, in the data files PropertyAliases.txt and PropertyValueAliases.txt.
>
> Many of the aliases have both a long form and a short form. For example, the General Category has a long alias “General_Category” and a short alias “gc”. The long alias is more comprehensible and is usually used in the text of the standard when referring to a particular character property. The short alias is more appropriate for use in regular expressions and other algorithmic contexts.

https://www.unicode.org/versions/Unicode17.0.0/core-spec/chapter-4/#G124142

> The Unicode Character Database defines a General_Category property for all Unicode code points. The General_Category value for a character serves as a basic classification of that character, based on its primary usage. The property extends the widely used subdivision of ASCII characters into letters, digits, punctuation, and symbols—a useful classification that needs to be elaborated and further subdivided to remain appropriate for the larger and more comprehensive scope of the Unicode Standard.

| Abbr | Long                  | Description                                                        |
|------|-----------------------|--------------------------------------------------------------------|
| Lu   | Uppercase_Letter      | an uppercase letter                                                |
| Ll   | Lowercase_Letter      | a lowercase letter                                                 |
| Lt   | Titlecase_Letter      | a digraph encoded as a single character, with first part uppercase |
| LC   | Cased_Letter          | Lu \| Ll \| Lt                                                     |
| Lm   | Modifier_Letter       | a modifier letter                                                  |
| Lo   | Other_Letter          | other letters, including syllables and ideographs                  |
| L    | Letter                | Lu \| Ll \| Lt \| Lm \| Lo                                         |
| Mn   | Nonspacing_Mark       | a nonspacing combining mark (zero advance width)                   |
| Mc   | Spacing_Mark          | a spacing combining mark (positive advance width)                  |
| Me   | Enclosing_Mark        | an enclosing combining mark                                        |
| M    | Mark                  | Mn \| Mc \| Me                                                     |
| Nd   | Decimal_Number        | a decimal digit                                                    |
| Nl   | Letter_Number         | a letterlike numeric character                                     |
| No   | Other_Number          | a numeric character of other type                                  |
| N    | Number                | Nd \| Nl \| No                                                     |
| Pc   | Connector_Punctuation | a connecting punctuation mark, like a tie                          |
| Pd   | Dash_Punctuation      | a dash or hyphen punctuation mark                                  |
| Ps   | Open_Punctuation      | an opening punctuation mark (of a pair)                            |
| Pe   | Close_Punctuation     | a closing punctuation mark (of a pair)                             |
| Pi   | Initial_Punctuation   | an initial quotation mark                                          |
| Pf   | Final_Punctuation     | a final quotation mark                                             |
| Po   | Other_Punctuation     | a punctuation mark of other type                                   |
| P    | Punctuation           | Pc \| Pd \| Ps \| Pe \| Pi \| Pf \| Po                             |
| Sm   | Math_Symbol           | a symbol of mathematical use                                       |
| Sc   | Currency_Symbol       | a currency sign                                                    |
| Sk   | Modifier_Symbol       | a non-letterlike modifier symbol                                   |
| So   | Other_Symbol          | a symbol of other type                                             |
| S    | Symbol                | Sm \| Sc \| Sk \| So                                               |
| Zs   | Space_Separator       | a space character (of various non-zero widths)                     |
| Zl   | Line_Separator        | U+2028 LINE SEPARATOR only                                         |
| Zp   | Paragraph_Separator   | U+2029 PARAGRAPH SEPARATOR only                                    |
| Z    | Separator             | Zs \| Zl \| Zp                                                     |
| Cc   | Control               | a C0 or C1 control code                                            |
| Cf   | Format                | a format control character                                         |
| Cs   | Surrogate             | a surrogate code point                                             |
| Co   | Private_Use           | a private-use character                                            |
| Cn   | Unassigned            | a reserved unassigned code point or a noncharacter                 |
| C    | Other                 | Cc \| Cf \| Cs \| Co \| Cn                                         |

\u0004 is EOT (control picture: ␄)

```console
ubuntu@laptop:~$ printf "\u0004\u0065\u0301\u000a"
é
```

```console
ubuntu@laptop:~$ printf "\u0004\u0065\u0301\u000a" | xxd
00000000: 0465 cc81 0a                             .e...
```

Normalize UTF-8 data using Unicode NFC:

```console
ubuntu@laptop:~$ printf "\u0004\u0065\u0301" | uconv -f utf8 -t utf8 -x '::nfc;' | xxd
00000000: 04c3 a9
```

Remove characters in general category Cc except for tab (\u0009), newline (\u000a), and carriage return (\u000d):


```console
ubuntu@laptop:~$ printf "\u0004\u0065\u0301\u000a" | uconv -x '[[:Cc:]-[\u0009\u000A\u000D]] > ;'
é
```


```console
ubuntu@laptop:~$ printf "\u0004\u0065\u0301\u000a" | uconv -x '[[:Cc:]-[\u0009\u000A\u000D]] > ; ::nfc;'
é
```

```console
ubuntu@laptop:~$ printf "\u0004\u0065\u0301\u000a" | uconv -x '[[:Cc:]-[\u0009\u000A\u000D]] > ; ::nfc;' | xxd
00000000: c3a9 0a
```
