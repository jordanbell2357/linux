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
In other words, how to capture terminal output.


## Alt+PrtSc

<kbd>Alt</kbd>+<kbd>PrtSc</kbd>

<img width="1363" height="732" alt="image" src="https://github.com/user-attachments/assets/1e1ab1d8-5bd0-47d4-8165-279435f15c5b" />


## script + ansilove

https://man7.org/linux/man-pages/man1/script.1.html

https://manpages.ubuntu.com/manpages/noble/en/man1/ansilove.1.html

```bash
script -O typescript -c "colortest-8" -q
```

```console
ubuntu@laptop:~$ ansilove -o colortest-8.png typescript
Input File: typescript
Output File: colortest-8.png
Font: 80x25
Bits: 8
Columns: 80

File typescript does not have a SAUCE record.
Processed in 0.008569 seconds.
```

<https://jordanbell.info/assets/images/colortest-8.png>

<img width="640" height="608" alt="colortest-8" src="https://github.com/user-attachments/assets/c6026e03-59ee-4ea4-884c-d97fe6f92cbe" />


```bash
script -O typescript -c "colortest-16" -q
ansilove -o colortest-16.png typescript
```

<https://jordanbell.info/assets/images/colortest-16.png>

<img width="640" height="1120" alt="colortest-16" src="https://github.com/user-attachments/assets/d36e144b-c05f-4ff9-b73a-2f4f9166a00d" />


```bash
script -O typescript -c "colortest-16b" -q
ansilove -o colortest-16b.png typescript
```

<https://jordanbell.info/assets/images/colortest-16b.png>

<img width="640" height="576" alt="colortest-16b" src="https://github.com/user-attachments/assets/3aa7c31e-a4be-4c1d-a009-ff1139a16fe9" />


```bash
script -O typescript -c "colortest-256" -q
ansilove -o colortest-256.png typescript
```

<https://jordanbell.info/assets/images/colortest-256.png>

## aha

https://manpages.ubuntu.com/manpages/noble/man1/aha.1.html

```bash
colortest-8 | aha -b -t colortest-8 > colortest-8.html
```

```bash
colortest-16 | aha -b -t colortest-16 > colortest-16.html
```

<https://jordanbell.info/assets/html/colortest-16.html>

```bash
colortest-16b | aha -b -t colortest-16b > colortest-16b.html
```

<https://jordanbell.info/assets/html/colortest-16b.html>


```bash
colortest-256 | aha -b -t colortest-256 > colortest-256.html
```

<https://jordanbell.info/assets/html/colortest-256.html>

## aha + wkhtmltopdf

https://wkhtmltopdf.org/

https://manpages.ubuntu.com/manpages/noble/man1/wkhtmltoimage.1.html

```bash
wkhtmltoimage colortest-8.html colortest-8.svg
```

<https://jordanbell.info/assets/images/colortest-8.svg>


```bash
wkhtmltoimage colortest-16.html colortest-16.svg
```

<https://jordanbell.info/assets/images/colortest-16.svg>


```bash
wkhtmltoimage colortest-16b.html colortest-16b.svg
```

<https://jordanbell.info/assets/images/colortest-16b.svg>

```console
wkhtmltoimage colortest-256.html colortest-256.svg
```

<https://jordanbell.info/assets/images/colortest-256.svg>


## xwd + ImageMagick convert

https://www.x.org/archive/X11R7.5/doc/man/man1/xwd.1.html

https://imagemagick.org/script/convert.php#gsc.tab=0

Terminal 1:

```bash
colortest-8
```

Terminal 2:

```bash
xwd -out xwd-8.xwd
```

Click on terminal 1. This creates file xwd-8.xwd. Then use ImageMagick convert.

```bash
convert xwd-8.xwd xwd-8.png
```

The same process is done for colortest-16, colortest-16b, colortest-256.

<https://jordanbell.info/assets/images/xwd-8.png>

<https://jordanbell.info/assets/images/xwd-16.png>

<https://jordanbell.info/assets/images/xwd-16b.png>

<https://jordanbell.info/assets/images/xwd-256.png>

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


## /dev/vcs

https://linux.die.net/man/4/vcs

https://manpages.ubuntu.com/manpages/noble/man1/screendump.1.html





## scrot

https://manpages.ubuntu.com/manpages/jammy/man1/scrot.1.html






## /dev/fb0

https://docs.kernel.org/fb/framebuffer.html

[fbgrab](https://github.com/GunnarMonell/fbgrab)


## asciinema


