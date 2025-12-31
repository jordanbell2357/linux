# colortest

https://github.com/pablopunk/colortest

https://manpages.ubuntu.com/manpages/noble/man1/colortest-8.1.html

https://manpages.ubuntu.com/manpages/noble/man1/colortest-16.1.html

https://manpages.ubuntu.com/manpages/noble/man1/colortest-16b.1.html

https://manpages.ubuntu.com/manpages/noble/man1/colortest-256.1.html


```bash
sudo apt install colortest
```

It became a question to explore, how to capture terminal output.
First, using Ctrl+PrtSc

```bash
colortest-8
```

<img width="1363" height="732" alt="image" src="https://github.com/user-attachments/assets/b2235e3a-27ec-4008-bde6-152c9d2897e9" />


Second, using script and ansilove [^aha]

[^aha]: Using aha: <https://jordanbell.info/assets/html/colortest-16.html>

```bash
script -q -c "colortest-16"
ansilove typescript
```

<img width="640" height="1120" alt="typescript" src="https://github.com/user-attachments/assets/0c8211d0-caa8-453a-b83c-aec76912a80e" />

Third, using aha

```bash
colortest-16b | aha -b > colortest-16b.html
```

<https://jordanbell.info/assets/html/colortest-16b.html>

Fourth, using script and ansilove

```bash
script -q -c "colortest-256"
ansilove -o colortest-256.png typescript
```

<img width="640" height="1216" alt="colortest-256" src="https://github.com/user-attachments/assets/914ea7ff-6177-40fa-a595-95a08f270ee0" />


