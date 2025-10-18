# script

<https://www.redhat.com/en/blog/linux-script-command>

```console
ubuntu@LAPTOP-JBell:~$ script out.log
Script started, output log file is 'out.log'.
ubuntu@LAPTOP-JBell:~$ cat </dev/tcp/time.nist.gov/13

60966 25-10-18 01:45:30 16 0 0 532.7 UTC(NIST) *
ubuntu@LAPTOP-JBell:~$ echo running \"exit\" will terminate script recording
running "exit" will terminate script recording
ubuntu@LAPTOP-JBell:~$ exit
exit
Script done.
ubuntu@LAPTOP-JBell:~$ cat out.log
Script started on 2025-10-17 21:45:22-04:00 [TERM="xterm-256color" TTY="/dev/pts/3" COLUMNS="120" LINES="30"]
ubuntu@LAPTOP-JBell:~$ cat </dev/tcp/time.nist.gov/13

60966 25-10-18 01:45:30 16 0 0 532.7 UTC(NIST) *
ubuntu@LAPTOP-JBell:~$ echo running \"exit\" will terminate script recording
running "exit" will terminate script recording
ubuntu@LAPTOP-JBell:~$ exit
exit

Script done on 2025-10-17 21:46:33-04:00 [COMMAND_EXIT_CODE="0"]
```
