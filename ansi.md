# ANSI escape sequences

Appendix H-1, https://nvlpubs.nist.gov/nistpubs/Legacy/FIPS/fipspub86.pdf

> ISO 6429 contains the following
> parameter values for use with SGR
> (Select Graphic Rendition) which are
> not present in ANSI X3.64-1979.

ECMA-48 Select Graphic Rendition (SGR), https://ecma-international.org/wp-content/uploads/ECMA-48_5th_edition_june_1991.pdf

https://man7.org/linux/man-pages/man4/console_codes.4.html

```bash
echo -e "\033[1;3;31;44mbold italic red display blue background\e[0m."
```

<span style="font-weight:bold;font-style:italic;color:red;background-color:blue;">bold italic red display blue background</span>.


| Command                                             | Display                                                           |
|-----------------------------------------------------|-------------------------------------------------------------------|
| <tt>echo -e "\033[1mbold\e[0m."</tt>                | <span style="font-weight:bold;">bold</span>.                      |
| <tt>echo -e "\033[3mitalic\e[0m."</tt>              | <span style="font-style:italic;">italic</span>.                   |
| <tt>echo -e "\033[4munderscore\e[0m."</tt>          | <span style="text-decoration:underline;">underscore</span>.       |
| <tt>echo -e "\033[30mblack\e[0m."</tt>              | <span style="color:dimgray;">black</span>.                        |
| <tt>echo -e "\033[31mred\e[0m."</tt>                | <span style="color:red;">red</span>.                              |
| <tt>echo -e "\033[32mgreen\e[0m."</tt>              | <span style="color:green;">green</span>.                          |
| <tt>echo -e "\033[33myellow\e[0m."</tt>             | <span style="color:olive;">yellow</span>.                         |
| <tt>echo -e "\033[34mblue\e[0m."</tt>               | <span style="color:blue;">blue</span>.                            |
| <tt>echo -e "\033[35mpurple\e[0m."</tt>             | <span style="color:purple;">purple</span>.                        |
| <tt>echo -e "\033[36mcyan\e[0m."</tt>               | <span style="color:teal;">cyan</span>.                            |
| <tt>echo -e "\033[37mwhite\e[0m."</tt>              | <span style="color:gray;">white</span>.                           |
| <tt>echo -e "\033[40mblack background\e[0m."</tt>   | <span style="background-color:black;">black background</span>.    |
| <tt>echo -e "\033[41mred background\e[0m."</tt>     | <span style="background-color:red;">red background</span>.        |
| <tt>echo -e "\033[42mgreen background\e[0m."</tt>   | <span style="background-color:green;">green background</span>.    |
| <tt>echo -e "\033[43myellow background\e[0m."</tt>  | <span style="background-color:olive;">yellow background</span>.   |
| <tt>echo -e "\033[44mblue background\e[0m."</tt>    | <span style="background-color:blue;">blue background</span>.      |
| <tt>echo -e "\033[45mmagenta background\e[0m."</tt> | <span style="background-color:purple;">magenta background</span>. |
| <tt>echo -e "\033[46mcyan background\e[0m."</tt>    | <span style="background-color:teal;">cyan background</span>.      |
| <tt>echo -e "\033[47mwhite background\e[0m."</tt>   | <span style="background-color:gray;">white background</span>.     |
