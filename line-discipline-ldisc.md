# Line discipline (LDISC)

https://lambdalambda.ninja/blog/56/

> While tty devices are mostly a "dumb" device, acting as a bidirectional channel between keyboard/console (master) and process (slave), there are a number of useful special semantics that have evolved over the years that suit the asymmetric, interactive terminal interface. Some well-known examples include:
>
> - Typed characters (input) show up on the console (output) by default even without any process printing this out. This is called *echoing*.
> - Backspacing in the input allows you to perform basic line editing. This type of line-based editing is called *cooked mode* or *canonical mode*. (We call it *raw mode* when cooked mode is disabled.)
> - Pressing the special interrupt control character, usually <kbd>Ctrl</kbd>+<kbd>C</kbd> (alternatively notated <kbd>^C</kbd>), sends a signal to the slave process.
> 
> Overall, this behavior is called the *line discipline*, and it describes the behavior ("policy") of the terminal device. Recall from the earlier blog post that the other major component of the tty/terminal subsystem is the terminal driver, which provides an interface to the input and output serial hardware devices ("mechanism"). All operations on a terminal device go through the line discipline interface.

https://www.linusakesson.net/programming/tty/

> **Line editing.** Most users make mistakes while typing, so a backspace key is often useful. This could of course be implemented by the applications themselves, but in accordance with the
> UNIX design philosophy, applications should be kept as simple as possible. So as a convenience, the operating system provides an editing buffer and some rudimentary editing commands
> (backspace, erase word, clear line, reprint), which are enabled by default inside the line discipline. Advanced applications may disable these features by putting the line discipline in *raw mode*
> instead of the default *cooked* (or *canonical*) mode. Most interactive applications (editors, mail user agents, shells, all programs relying on curses or readline) run in raw mode,
> and handle all the line editing commands themselves. The line discipline also contains options for character echoing and automatic conversion between carriage returns and linefeeds.
> Think of it as a primitive kernel-level sed(1), if you like.
