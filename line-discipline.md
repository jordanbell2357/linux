# Line discipline

https://docs.kernel.org/driver-api/tty/tty_ldisc.html

> TTY line discipline process all incoming and outgoing character from/to a tty device. The default line discipline is N_TTY. It is also a fallback if establishing any other discipline for a tty fails. If even N_TTY fails, N_NULL takes over. That never fails, but also does not process any characters -- it throws them away.

https://docs.kernel.org/driver-api/tty/n_tty.html

> The default (and fallback) TTY line discipline. It tries to handle characters as per POSIX.

https://lambdalambda.ninja/blog/56/

> While tty devices are mostly a "dumb" device, acting as a bidirectional channel between keyboard/console (master) and process (slave), there are a number of useful special semantics that have evolved over the years that suit the asymmetric, interactive terminal interface. Some well-known examples include:
>
> - Typed characters (input) show up on the console (output) by default even without any process printing this out. This is called *echoing*.
>   - Backspacing in the input allows you to perform basic line editing. This type of line-based editing is called *cooked mode* or *canonical mode*. (We call it *raw mode* when cooked mode is disabled.)
>   - Pressing the special interrupt control character, usually <kbd>Ctrl</kbd>+<kbd>C</kbd> (alternatively notated <kbd>^C</kbd>), sends a signal to the slave process.
> 
> Overall, this behavior is called the *line discipline*, and it describes the behavior ("policy") of the terminal device. Recall from the earlier blog post that the other major component of the tty/terminal subsystem is the terminal driver, which provides an interface to the input and output serial hardware devices ("mechanism"). All operations on a terminal device go through the line discipline interface.

https://www.linusakesson.net/programming/tty/

> A user types at a terminal (a physical teletype). This terminal is connected through a pair of wires to a *UART* (Universal Asynchronous Receiver and Transmitter) on the computer.
> The operating system contains a *UART driver* which manages the physical transmission of bytes, including parity checks and flow control.
> In a naïve system, the UART driver would then deliver the incoming bytes directly to some application process. But such an approach would lack the following essential features:
>
> **Line editing.** Most users make mistakes while typing, so a backspace key is often useful. This could of course be implemented by the applications themselves, but in accordance with the
> UNIX design philosophy, applications should be kept as simple as possible. So as a convenience, the operating system provides an editing buffer and some rudimentary editing commands
> (backspace, erase word, clear line, reprint), which are enabled by default inside the line discipline. Advanced applications may disable these features by putting the line discipline in *raw mode*
> instead of the default *cooked* (or *canonical*) mode. Most interactive applications (editors, mail user agents, shells, all programs relying on curses or readline) run in raw mode,
> and handle all the line editing commands themselves. The line discipline also contains options for character echoing and automatic conversion between carriage returns and linefeeds.
> Think of it as a primitive kernel-level sed(1), if you like.
>
>  Incidentally, the kernel provides several different line disciplines. Only one of them is attached to a given serial device at a time.
> The default discipline, which provides line editing, is called N_TTY (drivers/char/n_tty.c, if you're feeling adventurous).
> Other disciplines are used for other purposes, such as managing packet switched data (ppp, IrDA, serial mice), but that is outside the scope of this article.
>
> **Session management.** The user probably wants to run several programs simultaneously, and interact with them one at a time. If a program goes into an endless loop, the user may want
> to kill it or suspend it. Programs that are started in the background should be able to execute until they try to write to the terminal, at which point they should be suspended.
> Likewise, user input should be directed to the foreground program only. The operating system implements these features in the TTY driver (drivers/char/tty_io.c).
>
> An operating system process is "alive" (has an *execution context*), which means that it can perform actions.
> The TTY driver is not alive; in object oriented terminology, the TTY driver is a passive object.
> It has some data fields and some methods, but the only way it can actually do something is when one of its methods gets called from the context of a process or a kernel interrupt handler.
> The line discipline is likewise a passive entity.
>
> Together, a particular triplet of UART driver, line discipline instance and TTY driver may be referred to as a *TTY device*, or sometimes just TTY.
> A user process can affect the behaviour of any TTY device by manipulating the corresponding device file under /dev.
> Write permissions to the device file are required, so when a user logs in on a particular TTY, that user must become the owner of the device file.
> This is traditionally done by the login(1) program, which runs with root privileges.
