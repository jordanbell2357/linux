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

<img width="640" height="608" alt="colortest-8" src="https://github.com/user-attachments/assets/c6026e03-59ee-4ea4-884c-d97fe6f92cbe" />


```bash
script -O typescript -c "colortest-16" -q
ansilove -o colortest-16.png typescript
```

<img width="640" height="1120" alt="colortest-16" src="https://github.com/user-attachments/assets/d36e144b-c05f-4ff9-b73a-2f4f9166a00d" />


```bash
script -O typescript -c "colortest-16b" -q
ansilove -o colortest-16b.png typescript
```

<img width="640" height="576" alt="colortest-16b" src="https://github.com/user-attachments/assets/3aa7c31e-a4be-4c1d-a009-ff1139a16fe9" />


```bash
script -O typescript -c "colortest-256" -q
ansilove -o colortest-256.png typescript
```

<img width="640" height="1216" alt="colortest-256" src="https://github.com/user-attachments/assets/4c41a0c3-5288-4601-8ab5-11b6469648b2" />


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

https://jordanbell.info/assets/colortest-8.svg


```bash
wkhtmltoimage colortest-16.html colortest-16.svg
```

https://jordanbell.info/assets/colortest-16.svg


```bash
wkhtmltoimage colortest-16b.html colortest-16b.svg
```

https://jordanbell.info/assets/colortest-16b.svg

```console
wkhtmltoimage colortest-256.html colortest-256.svg
```

https://jordanbell.info/assets/colortest-256.svg


## ImageMagick

https://imagemagick.org/script/import.php#gsc.tab=0



## scrot

https://manpages.ubuntu.com/manpages/jammy/man1/scrot.1.html


## shutter

https://shutter-project.org/

## xwd

https://www.x.org/archive/X11R7.5/doc/man/man1/xwd.1.html

https://www.x.org/archive/X11R7.7/doc/man/man1/xwud.1.xhtml


## /dev/vcs

https://linux.die.net/man/4/vcs

https://manpages.ubuntu.com/manpages/noble/man1/screendump.1.html


## /dev/fb0

https://docs.kernel.org/fb/framebuffer.html

[fbgrab](https://github.com/GunnarMonell/fbgrab)


## asciinema


