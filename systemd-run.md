# systemd-run

<https://serverfault.com/a/979654/1320629>

<https://www.freedesktop.org/software/systemd/man/latest/systemd-run.html>


```bash
systemd-run -p MemoryMax=500M -t bash -c 'dd if=/dev/zero bs=100M count=100 | tail > /dev/null'
```

```console
==== AUTHENTICATING FOR org.freedesktop.systemd1.manage-units ====
Authentication is required to manage system services or other units.
Authenticating as: Ubuntu (ubuntu)
Password:
==== AUTHENTICATION COMPLETE ====
Running as unit: run-u107.service
Press ^] three times within 1s to disconnect TTY.
ubuntu@histfile:~$ sudo systemctl status run-u107.service
× run-u107.service - /usr/bin/bash -c "dd if=/dev/zero bs=100M count=100 | tail > /dev/null"
     Loaded: loaded (/run/systemd/transient/run-u107.service; transient)
  Transient: yes
     Active: failed (Result: oom-kill) since Sat 2025-12-06 20:07:00 UTC; 20s ago
   Duration: 693ms
    Process: 11522 ExecStart=/usr/bin/bash -c dd if=/dev/zero bs=100M count=100 | tail > /dev/null (code=killed, signal>
   Main PID: 11522 (code=killed, signal=TERM)
        CPU: 1.053s

Dec 06 20:06:59 histfile systemd[1]: Started run-u107.service - /usr/bin/bash -c "dd if=/dev/zero bs=100M count=100 | t>
Dec 06 20:07:00 histfile systemd[1]: run-u107.service: A process of this unit has been killed by the OOM killer.
Dec 06 20:07:00 histfile systemd[1]: run-u107.service: Failed with result 'oom-kill'.
Dec 06 20:07:00 histfile systemd[1]: run-u107.service: Consumed 1.053s CPU time, 500.0M memory peak, 0B memory swap pea>
```


```bash
systemd-run -p MemoryMax=2G -t bash -c "dd if=/dev/zero bs=100M count=100 | tail > /dev/null"
```

```console
==== AUTHENTICATING FOR org.freedesktop.systemd1.manage-units ====
Authentication is required to manage system services or other units.
Authenticating as: Ubuntu (ubuntu)
Password:
==== AUTHENTICATION COMPLETE ====
Running as unit: run-u113.service; invocation ID: 1eda47c044614a549533b3bf8f8b5ac6
Press ^] three times within 1s to disconnect TTY.
ubuntu@histfile:~$ sud osystemctl status run-u113.service
Command 'sud' not found, but there are 15 similar ones.
ubuntu@histfile:~$ sudo systemctl status run-u113.service
× run-u113.service - /usr/bin/bash -c "dd if=/dev/zero bs=100M count=100 | tail > /dev/null"
     Loaded: loaded (/run/systemd/transient/run-u113.service; transient)
  Transient: yes
     Active: failed (Result: oom-kill) since Sat 2025-12-06 20:11:06 UTC; 16s ago
   Duration: 3.342s
    Process: 11597 ExecStart=/usr/bin/bash -c dd if=/dev/zero bs=100M count=100 | tail > /dev/null (code=killed, signal>
   Main PID: 11597 (code=killed, signal=TERM)
        CPU: 5.113s

Dec 06 20:11:02 histfile systemd[1]: Started run-u113.service - /usr/bin/bash -c "dd if=/dev/zero bs=100M count=100 | t>
Dec 06 20:11:05 histfile systemd[1]: run-u113.service: A process of this unit has been killed by the OOM killer.
Dec 06 20:11:06 histfile systemd[1]: run-u113.service: Failed with result 'oom-kill'.
Dec 06 20:11:06 histfile systemd[1]: run-u113.service: Consumed 5.113s CPU time, 2.0G memory peak, 0B memory swap peak.
```
