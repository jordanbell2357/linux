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

| Command                                    |
|--------------------------------------------|
| echo -e "\033[1mbold\e[0m."                |
| echo -e "\033[3mitalic\e[0m."              |
| echo -e "\033[4munderscore\e[0m."          |
| echo -e "\033[30mblack\e[0m."              |
| echo -e "\033[31mred\e[0m."                |
| echo -e "\033[32mgreen\e[0m."              |
| echo -e "\033[33myellow\e[0m."             |
| echo -e "\033[34mblue\e[0m."               |
| echo -e "\033[35mpurple\e[0m."             |
| echo -e "\033[36mcyan\e[0m."               |
| echo -e "\033[37mwhite\e[0m."              |
| echo -e "\033[40mblack background\e[0m."   |
| echo -e "\033[41mred background\e[0m."     |
| echo -e "\033[42mgreen background\e[0m."   |
| echo -e "\033[43myellow background\e[0m."  |
| echo -e "\033[44mblue background\e[0m."    |
| echo -e "\033[45mmagenta background\e[0m." |
| echo -e "\033[46mcyan background\e[0m."    |
| echo -e "\033[47mwhite background\e[0m."   |
