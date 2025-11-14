# tee

Let's use tee [^tee] to write output as root, and take this as a chance to review this pattern.

[^tee]: <https://pubs.opengroup.org/onlinepubs/000095399/utilities/tee.html>

```console
ubuntu@vps-9e6a8f0e:~$ echo bob | sudo cat > bob1; ls -l bob1
-rw-rw-r-- 1 ubuntu ubuntu 4 Nov 10 23:55 bob1
```

compared to

```console
ubuntu@vps-9e6a8f0e:~$ echo bob | sudo tee -a bob2; ls -l bob2
bob
-rw-r--r-- 1 root root 4 Nov 11 00:08 bob2
```

or to eliminate standard output

```console
ubuntu@vps-9e6a8f0e:~$ echo bob | sudo tee -a bob2 1> /dev/null; ls -l bob2
-rw-r--r-- 1 root root 4 Nov 11 00:09 bob2
```

We want a program with super user privileges to create a file, not a redirection from a Bash session being run as a regular user. We could instead use `sudo bash -c` thus

```console
ubuntu@vps-9e6a8f0e:~$ sudo bash -c "echo bob > bob3"; ls -l bob3
-rw-r--r-- 1 root root 4 Nov 11 00:19 bob3
```

```console
ubuntu@vps-9e6a8f0e:~$ echo AllowUsers ubuntu | sudo tee -a /etc/ssh/sshd_config
AllowUsers ubuntu
ubuntu@vps-9e6a8f0e:~$ tail -n 1 /etc/ssh/sshd_config
AllowUsers ubuntu
```
