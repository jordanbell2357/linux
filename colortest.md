# colortest

https://github.com/pablopunk/colortest

https://manpages.ubuntu.com/manpages/noble/man1/colortest-8.1.html

https://manpages.ubuntu.com/manpages/noble/man1/colortest-16.1.html

https://manpages.ubuntu.com/manpages/noble/man1/colortest-16b.1.html

https://manpages.ubuntu.com/manpages/noble/man1/colortest-256.1.html

```bash
sudo apt install colortest
```

We use colortest as a place to examine ways to take screenshots in Linux.
In other words, how to capture terminal output.


## Alt+PrtSc

<kbd>Alt</kbd>+<kbd>PrtSc</kbd>

```bash
colortest-256
```

<img width="1363" height="732" alt="image" src="https://github.com/user-attachments/assets/1e1ab1d8-5bd0-47d4-8165-279435f15c5b" />


## script and ansilove

https://man7.org/linux/man-pages/man1/script.1.html

https://manpages.ubuntu.com/manpages/noble/en/man1/ansilove.1.html


```bash
script -q -c "colortest-16"
ansilove typescript
```

<img width="640" height="1120" alt="typescript" src="https://github.com/user-attachments/assets/0c8211d0-caa8-453a-b83c-aec76912a80e" />


```bash
script -q -c "colortest-256"
ansilove -o colortest-256.png typescript
```

<img width="640" height="1216" alt="colortest-256" src="https://github.com/user-attachments/assets/914ea7ff-6177-40fa-a595-95a08f270ee0" />



## aha

```bash
colortest-16 | aha -b > colortest-16.html
```

<https://jordanbell.info/assets/html/colortest-16.html>

```bash
colortest-16b | aha -b > colortest-16b.html
```

<https://jordanbell.info/assets/html/colortest-16b.html>

