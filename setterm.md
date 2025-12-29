# setterm

https://tldp.org/HOWTO/html_single/Text-Terminal-HOWTO/Text-Terminal-HOWTO.html#toc17.14

> The terminal settings are normally set once when the terminal is installed using the setup procedures in the terminal manual.
> However, some settings may be changed when the terminal is in use. You normally would not give any "stty" or "setserial"
> commands when the terminal is in use as they are likely to corrupt the terminal interface.
> However, there are changes you may make to the appearance of the terminal screen or to its behavior without destroying the integrity of the interface.
> Sometimes these changes are made automatically by application programs so you may not need to deal with them.
>
> One direct method of making such changes is to use the setup key (or the like) at the terminal and then use menus (or the like) to make the changes. To do this you may need to be familiar with the terminal. The other 3 methods send an escape sequence from the computer to the terminal to make the changes. These 3 examples show different methods of doing this to set reverse video:
>
> 1. setterm -reverse
> 2. tput -rev
> 3. echo ^[[7m
>
> **setterm** 
> This is the easiest command to use. It uses long options (but doesn't use the normal -- before them). It consults the terminfo database to determine what code to send.
> You may change the color, brightness, linewrap, keyboard repeat, cursor appearance, etc.
>
> **tput** 
> The "tput" command is similar to "setterm" but instead of using ordinary words as arguments, you must use the abbreviations used by terminfo. Many of the abbreviations are quite terse and hard to remember.
>
> **echo** 
> In the example "echo ^[[7m" to set reverse video, the ^[ is the escape character. To type it type ^V^[ (or ^V followed by the escape key).
> To use this "echo" method you must find out what code to use from a terminal manual or from terminfo or termcap.
> It's simpler to use setterm or tput if you are typing on the command line.
> Since "echo ..." will execute faster (since it doesn't do any lookups) it's good for using in shell scripts which run at start-up, etc.

```bash
echo $(setterm --reverse on; printf "reversed text"; setterm --reverse off); echo "normal text"
```


https://man7.org/linux/man-pages/man1/setterm.1.html

```bash
echo $(setterm --foreground magenta; printf "magenta text"; setterm --foreground default); echo "normal text"
```
