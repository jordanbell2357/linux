# tput

https://linuxcommand.org/lc3_adv_tput.php

https://ss64.com/bash/tput.html

> Set terminal-dependent capabilities, colour, position.

```
   capname
           Indicates the capability from the terminfo database.
           When termcap  support is compiled in, the termcap name for the capability
           is also accepted.
           Typical capabilities include:
             tput setab colour  Set ANSI Background colour
             tput setaf colour  Set ANSI Foreground colour
             tput blink   Set blink mode
             tput bold    Set bold mode
             tput dim     Set half-bright mode
             tput smul    Set underline mode
             tput rmul    Exit underline mode
             tput rev     Reverse mode
             tput smso    Set standout mode
             tput rmso    Exit standout mode
             tput sgr0    Reset all attributes
             tput cols    Display the number of columns
             tput lines   Display the number of lines
```


<div style="color:white; background-color:black">
<pre>
<span style="text-decoration:underline;">This text is underlined (smul). </span>
</pre>
</div>

<div style="color:white; background-color:black">
<pre>
</pre>
</div>

<div style="color:white; background-color:black">
<pre>
This text is white.
</pre>
</div>
