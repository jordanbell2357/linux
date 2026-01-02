# vttest

https://invisible-island.net/vttest/

We use vttest as an occasion to use different screen recording or video capture programs.


## script

https://man7.org/linux/man-pages/man1/script.1.html

https://man7.org/linux/man-pages/man1/scriptreplay.1.html

```console
ubuntu@laptop:~$ tty
/dev/pts/0
ubuntu@laptop:~$ script -T script-vttest-log -q script-vttest
ubuntu@laptop:~$ tty
/dev/pts/2
ubuntu@laptop:~$ vttest
```

We end the script session pressing <kbd>Ctrl</kbd>+<kbd>d</kbd>.


```bash
script -T script-vttest-log -q script-vttest
```

We run `scriptreplay` to view the script session.

```bash
scriptreplay -T script-vttest-log -O script-vttest
```


## ttyrec

http://0xcc.net/ttyrec/

https://github.com/mjording/ttyrec

https://github.com/ovh/ovh-ttyrec

https://manpages.ubuntu.com/manpages/noble/man1/ttyrec.1.html

https://manpages.ubuntu.com/manpages/noble/man1/ttyplay.1.html

```bash
ttyrec ttyrec-vttest.tty
vttest
```

https://rlgallery.org/about/ttyrec.html

> TTYREC files are recordings of text-based sessions, much like screencasts are recordings of graphical sessions. The Roguelike Gallery and other roguelike sites create ttyrec recordings of games played online, so that others can watch them.

These ttyrec files can then be played using ttyplay, e.g.

```bash
ttyplay ttyrec-vttest-2.tty
```

<https://jordanbell.info/assets/videos/ttyrec-vttest-2.tty>


## ipbt

https://manpages.ubuntu.com/manpages/noble/man1/ipbt.1.html

```bash
sudo apt install its-playback-time
```

Display ttyrec-vttest-2.tty by running

```bash
ipbt ttyrec-vttest-2.tty
```

and then pressing <kbd>Space</kbd> to progress through frames.


## Tera Term

https://github.com/TeraTermProject/teraterm

https://teratermproject.github.io/manual/5/ja/

https://teratermproject.github.io/manual/5/en/usage/ttyrec.html

> The TTXttyrec plug-in records the screen buffer as a binary file. Select the TTY Record under File menu and the saving dialog is shown. Specify a file on the dialog and the recording will start. Again, select the TTY Record entry and the recording will stop.
>
> This plug-in supports for recording the serial console. However, the Tera Term 4.60 or later needs to do it. So, the Tera Term before 4.60 supports this plug-in and only TCP connection.
>
> The TTXttyplay plug-in replays the data recorded by the TTXttyrec plug-in. Select the TTY Replay under File menu and the opening dialog is shown. specify a recorded file and the recorded data will replay. The Tera Term 4.60 or later needs to use the TTXttyplay plug-in.
>
> The data format is same as the ttyrec. The data recorded by the TTXttyrec plug-in can replay by using the ttyplay command. The data recorded by the ttyrec command can replay by using the TTXttyplay plug-in.


