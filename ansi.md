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


