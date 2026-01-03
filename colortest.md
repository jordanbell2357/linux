# colortest

https://github.com/pablopunk/colortest

https://manpages.ubuntu.com/manpages/noble/man1/colortest-8.1.html

https://manpages.ubuntu.com/manpages/noble/man1/colortest-16.1.html

https://manpages.ubuntu.com/manpages/noble/man1/colortest-16b.1.html

https://manpages.ubuntu.com/manpages/noble/man1/colortest-256.1.html

```bash
sudo apt install colortest
```

We use colortest as an occasion to examine ways to take screenshots in Linux.
In other words, how to capture static terminal output. Another place,
we will use vttest as an occasion to examine
ways to take screencasts, or videos, in Linux.

We use WSL in Windows, and Ubuntu as a virtual machine using VirtualBox, Hyper-V Manager,
and VMWare Workstation.


## Windows

WSL

<kbd>Alt</kbd>+<kbd>PrtSc</kbd>

<https://jordanbell.info/assets/images/wsl2-alt-prtsc-256.png>

## GNOME

GNOME on Ubuntu on Hyper-V:

https://help.ubuntu.com/stable/ubuntu-help/screen-shot-record.html

https://help.gnome.org/gnome-help/screen-shot-record.html

https://wiki.debian.org/ScreenShots

<kbd>Shift</kbd>+<kbd>PrtSc</kbd> takes screenshot of entire screen and saves file to file like `~/Pictures/Screenshots/Screenshot from 2025-12-31 19-33-19.png`. If two screenshots are taken
within the same second, the others are named with an additional hyphen and number like `Screenshot from 2025-12-31 19-33-19-1.png`.

<kbd>PrtSc</kbd> gives interactive tool to select window, region, or entire screen.

We show this for colortest-16 and colortest-256.

<https://jordanbell.info/assets/images/gnome-prtsc-16.png>

<https://jordanbell.info/assets/images/gnome-prtsc-256.png>


## GNOME Screenshot

https://linux.die.net/man/1/gnome-screenshot

GNOME on Ubuntu on Hyper-V:: Installing gnome-screenshot lets us invoke it from the command line with options.

`-w` captures current window:

```bash
gnome-screenshot -w
```

`-i` runs interactively:

```bash
gnome-screenshot -i
```

<https://jordanbell.info/assets/images/gnome-screenshot-8-i.png>


## GNU Screen

https://www.gnu.org/software/screen/manual/screen.html#Hardcopy

> **Command: hardcopy *[-h]* *[file]***
>
> (*C-a* *h*)
> 
> Writes out the currently displayed image to the file *file*, or, if no filename is specified, to **hardcopy.*n*** in the default directory, where *n* is the number of the current window. This either appends or overwrites the file if it exists, as determined by the **hardcopy_append** command. If the option **-h** is specified, dump also the contents of the scrollback buffer.

We run screen and run colortest-8 in the screen session.

We press <kbd>Ctrl</kbd>+<kbd>a</kbd>, then <kbd>:</kbd>, then `hardcopy -h screen-8.txt`.

The file `screen-8.txt` is the text in the scrollback color, without color. We end the screen session using <kbd>Ctrl</kbd>+<kbd>d</kbd>

<https://jordanbell.info/assets/images/screen-8.txt>

We do the same for colortest-16b.

<https://jordanbell.info/assets/images/screen-16b.txt>


## script + ansilove

https://man7.org/linux/man-pages/man1/script.1.html

https://manpages.ubuntu.com/manpages/noble/en/man1/ansilove.1.html

The output of *script* is text with escape sequences and control sequences, namely "ANSI".

```bash
script -O typescript-8 -c "colortest-8" -q
```

```console
ubuntu@vm:~/Desktop$ ansilove -o ansilove-8.png typescript-8
Input File: typescript-8
Output File: ansilove-8.png
Font: 80x25
Bits: 8
Columns: 80

File typescript-8 does not have a SAUCE record.

Processed in 0.004059 seconds.
```

<https://jordanbell.info/assets/images/ansilove-8.png>


```bash
script -O typescript-16 -c "colortest-16" -q
ansilove -o ansilove-16.png typescript-16
```

<https://jordanbell.info/assets/images/ansilove-16.png>

```bash
script -O typescript-16b -c "colortest-16b" -q
ansilove -o ansilove-16b.png typescript-16b
```

<https://jordanbell.info/assets/images/ansilove-16b.png>

```bash
script -O typescript-256 -c "colortest-256" -q
ansilove -o ansilove-256.png typescript-256
```

<https://jordanbell.info/assets/images/ansilove-256.png>

<https://jordanbell.info/assets/images/typescript-8>

<https://jordanbell.info/assets/images/typescript-16>

<https://jordanbell.info/assets/images/typescript-16b>

<https://jordanbell.info/assets/images/typescript-256>


## script + textimg

https://github.com/jiro4989/textimg

```bash
wget https://github.com/jiro4989/textimg/releases/download/v3.1.9/textimg_3.1.9_amd64.deb
sudo dpkg -i ./*.deb
```

We use the typescript (ANSI) output of *script*:

```bash
script -O typescript-8 -c "colortest-8" -q
script -O typescript-16 -c "colortest-16" -q
script -O typescript-16b -c "colortest-16b" -q
script -O typescript-256 -c "colortest-256" -q
```

Then we make images from these typescript files using *textimg*.

```bash
textimg -o textimg-8.png < typescript-8
textimg -o textimg-16.png < typescript-16
textimg -o textimg-16b.png < typescript-16b
textimg -o textimg-256.png < typescript-256
```

## xterm

https://invisible-island.net/xterm/manpage/xterm.html

https://stackoverflow.com/questions/29987557/xterm-dump-of-full-scrollable-window-content

```bash
xterm -l -lf xterm-8.ans
```

This opens an xterminal window. In it we run colortest and exit, and this creates a text file
with ANSI escape codes, xterm-8.ans. We do the same for colortest-16, colortest-16b, colortest-256.

<https://jordanbell.info/assets/images/xterm-8.ans>

<https://jordanbell.info/assets/images/xterm-16.ans>

<https://jordanbell.info/assets/images/xterm-16b.ans>

<https://jordanbell.info/assets/images/xterm-256.ans>

These can be viewed using cat in Linux and in Windows using cat in PowerShell.

<https://jordanbell.info/assets/images/powershell-8.png>


## Ansifilter

https://manpages.ubuntu.com/manpages/jammy/man1/ansifilter.1.html

http://andre-simon.de/doku/ansifilter/en/ansifilter.php

Using Ansifilter Windows GUI with TTY colortest-8 and colortest-16b output.

<https://jordanbell.info/assets/images/ansifilter-gui-8.png>

<https://jordanbell.info/assets/images/ansifilter-gui-16b.png>

Using Ansifilter with xterm output.

```bash
ansifilter -i xterm-8.ans -o ansifilter-8.html --html
ansifilter -i xterm-16.ans -o ansifilter-16.html --html
ansifilter -i xterm-16b.ans -o ansifilter-16b.html --html
ansifilter -i xterm-256.ans -o ansifilter-256.html --html
```


## ANSiMat

https://sourceforge.net/projects/ansimat/

We run ansimat.exe in Windows PowerShell.

```
.\ansimat.exe typescript-8
```

```
.\ansimat.exe typescript-16
```

<https://jordanbell.info/assets/images/ansimat-8.png>

<https://jordanbell.info/assets/images/ansimat-16.png>


## ASCII Art Studio

https://www.torchsoft.com/en/aas_information.html

Windows GUI

We show the display of typescript-8 and typescript-16 in ASCII Art Studio and then show the exported images made by ASCII Art Studio.

<https://jordanbell.info/assets/images/asciistudio-8.png>

<https://jordanbell.info/assets/images/asciistudio-16.png>

<https://jordanbell.info/assets/images/asciistudio-8-export.gif>

<https://jordanbell.info/assets/images/asciistudio-16-export.gif>


## PabloDraw

https://github.com/cwensley/pablodraw

Windows GUI

It requires us to have file extensions to open a file. We demonstrate copying typescript-8 to typescript-8.ans and opening in PabloDraw.

<https://jordanbell.info/assets/images/pablodraw-8.png>


## Moebius

https://blocktronics.github.io/moebius/

Windows GUI

We demonstrate with typescript-8 and typescript-16. We show the files viewed in Moebius and also supply the PNG exports Moebius can make of ANSI files.

<https://jordanbell.info/assets/images/moebius-8.png>

<https://jordanbell.info/assets/images/moebius-16.png>

<https://jordanbell.info/assets/images/moebius-export-8.png>

<https://jordanbell.info/assets/images/moebius-export-16.png>


## aha

https://manpages.ubuntu.com/manpages/noble/man1/aha.1.html

```bash
colortest-8 | aha -b -t colortest-8 > aha-8.html
```

<https://jordanbell.info/assets/html/aha-8.html>

```bash
colortest-16 | aha -b -t colortest-16 > aha-16.html
```

<https://jordanbell.info/assets/html/aha-16.html>

```bash
colortest-16b | aha -b -t colortest-16b > aha-16b.html
```

<https://jordanbell.info/assets/html/aha-16b.html>


```bash
colortest-256 | aha -b -t colortest-256 > aha-256.html
```

<https://jordanbell.info/assets/html/aha-256.html>


## aha + wkhtmltoimage

https://wkhtmltopdf.org/

https://manpages.ubuntu.com/manpages/noble/man1/wkhtmltoimage.1.html

```bash
wkhtmltoimage aha-8.html wkhtmltoimage-8.svg
```

<https://jordanbell.info/assets/images/wkhtmltoimage-8.svg>


```bash
wkhtmltoimage aha-16.html wkhtmltoimage-16.svg
```

<https://jordanbell.info/assets/images/wkhtmltoimage-16.svg>


```bash
wkhtmltoimage aha-16b.html wkhtmltoimage-16b.svg
```

<https://jordanbell.info/assets/images/wkhtmltoimage-16b.svg>

```bash
wkhtmltoimage aha-256.html wkhtmltoimage-256.svg
```

<https://jordanbell.info/assets/images/wkhtmltoimage-256.svg>


## xwd + ImageMagick convert

https://www.x.org/archive/X11R7.5/doc/man/man1/xwd.1.html

https://www.x.org/archive/X11R7.5/doc/man/man1/xwud.1.html

https://imagemagick.org/script/convert.php#gsc.tab=0

Terminal 1:

```bash
colortest-8
```

Terminal 2:

```bash
xwd -out xwd-8.xwd
```

Click on terminal 1. This creates file xwd-8.xwd and the program xwd terminates successfully. Then use ImageMagick convert.

```bash
convert xwd-8.xwd xwd-8.png
```

The same process is done for colortest-16, colortest-16b, colortest-256.

<https://jordanbell.info/assets/images/xwd-8.xwd>

<https://jordanbell.info/assets/images/xwd-16.xwd>

<https://jordanbell.info/assets/images/xwd-16b.xwd>

<https://jordanbell.info/assets/images/xwd-256.xwd>

<https://jordanbell.info/assets/images/xwd-8.png>

<https://jordanbell.info/assets/images/xwd-16.png>

<https://jordanbell.info/assets/images/xwd-16b.png>

<https://jordanbell.info/assets/images/xwd-256.png>

*xwud* is a native viewer of *xwd* output.

```bash
xwud xwd-256.xwd
```

<https://jordanbell.info/assets/images/xwud-256.png>

## Flameshot

https://flameshot.org/docs/installation/installation-linux/

Running `flameshot` in xterm opens Flameshot in the system tray in GNOME, which can be used interactively.

Running `flamegui gui` in xterm opens the interactive interface.

We select a region of the display to capture.

```console
ubuntu@vm:~/Desktop$ flameshot gui
flameshot: info: Capture saved as /home/ubuntu/Desktop/flameshot-8.png
```

<https://jordanbell.info/assets/images/flameshot-8.png>


## ImageMagick import

https://imagemagick.org/script/import.php#gsc.tab=0

Terminal 1:

```bash
colortest-256
```

```bash
import import-256.png
```

We can either click on window, or select region.

<https://jordanbell.info/assets/images/import-256.png>

The same can be done for colortest-8, colortest-16, colortest-16b but we haven't.


## shutter

https://shutter-project.org/faq-help/man-page/

Terminal 1 runs colortest.

Terminal 2 runs shutter. We select window for terminal 1.

```bash
shutter -w -o shutter-8.png
shutter -w -o shutter-16.png
shutter -w -o shutter-16b.png
shutter -w -o shutter-256.png
```

<https://jordanbell.info/assets/images/shutter-8.png>

<https://jordanbell.info/assets/images/shutter-16.png>

<https://jordanbell.info/assets/images/shutter-16b.png>

<https://jordanbell.info/assets/images/shutter-256.png>


## scrot

https://manpages.ubuntu.com/manpages/jammy/man1/scrot.1.html

We run colortest in terminal 1. Then in terminal 2 we run scrot, and can either select an entire window or select a region in X11.

```bash
scrot -s scrot-256.png
```

<https://jordanbell.info/assets/images/scrot-256.png>


## gtk-vector-screenshot

https://github.com/nomeata/gtk-vector-screenshot

In one xterm we run colortest and in another we run `take-vector-screenshot`. We click on the first xterm window and save the screenshot as PDF.

```bash
take-vector-screenshot
```

<https://jordanbell.info/assets/images/gtk-vector-screenshot-8.pdf>

<https://jordanbell.info/assets/images/gtk-vector-screenshot-16.pdf>

<https://jordanbell.info/assets/images/gtk-vector-screenshot-16b.pdf>

<https://jordanbell.info/assets/images/gtk-vector-screenshot-256.pdf>


## /dev/vcs

https://linux.die.net/man/4/vcs

https://manpages.ubuntu.com/manpages/noble/man1/screendump.1.html

https://man7.org/linux/man-pages/man1/setterm.1.html

We run Ubuntu using VirtualBox. We login to tty1 and run colortest-8.
The following is a screenshot taken using VirtualBox:

<https://jordanbell.info/assets/images/vcs-tty1.png>

We switch to tty2 by <kbd>Fn</kbd>+<kbd>Alt</kbd>+<kbd>F2</kbd>, login
and run

```bash
sudo cat /dev/vcs1
```

or

```bash
sudo screendump 1
```

or

```bash
sudo setterm --dump 1
```

It shows the text output currently displayed on tty1, without color.

The following is a screenshot taken using VirtualBox:

<https://jordanbell.info/assets/images/vcs-tty2.png>


## /dev/fb0

https://docs.kernel.org/fb/framebuffer.html

https://github.com/jwilk/fbcat

https://github.com/GunnarMonell/fbgrab

https://askubuntu.com/questions/12208/can-i-take-a-screenshot-of-a-virtual-console


We use Ubuntu Desktop on VMWare Workstation.
From X11, we access a virtual console pressing <kbd>Fn</kbd>+<kbd>Ctrl</kbd>+<kbd>Alt</kbd>+<kbd>F3</kbd>, to get to tty3.
We run colortest-8 in tty3.

Then we enter tty4 using <kbd>Fn</kbd>+<kbd>Alt</kbd>+<kbd>F4</kbd>. We run 

```bash
sudo fbgrab -c 3 fbgrab-8.png
```

<https://jordanbell.info/assets/images/fbgrab-8.png>

<https://jordanbell.info/assets/images/fbgrab-16.png>

<https://jordanbell.info/assets/images/fbgrab-16b.png>

<https://jordanbell.info/assets/images/fbgrab-256.png>

We also use `fbcat` directly in tty3.

```bash
colortest-8
sudo fbcat > fbcat-8.ppm
```

and likewise for the other colortest programs. After each execution, we
press <kbd>Ctrl</kbd>+<kbd>l</kbd>.

<https://jordanbell.info/assets/images/fbcat-8.ppm>

<https://jordanbell.info/assets/images/fbcat-16.ppm>

<https://jordanbell.info/assets/images/fbcat-16b.ppm>

<https://jordanbell.info/assets/images/fbcat-256.ppm>



