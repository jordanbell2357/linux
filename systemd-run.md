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
Running as unit: run-u33.service; invocation ID: e4142a5a924140aab7544068d1f80a74
Press ^] three times within 1s to disconnect TTY.
```

```bash
sudo systemctl status --no-pager -l 
```

```console
× run-u36.service - /usr/bin/bash -c "dd if=/dev/zero bs=100M count=100 | tail > /dev/null"
     Loaded: loaded (/run/systemd/transient/run-u36.service; transient)
  Transient: yes
     Active: failed (Result: oom-kill) since Sun 2025-12-07 05:45:05 UTC; 18s ago
   Duration: 710ms
    Process: 2201 ExecStart=/usr/bin/bash -c dd if=/dev/zero bs=100M count=100 | tail > /dev/null (code=killed, signal=TERM)
   Main PID: 2201 (code=killed, signal=TERM)
        CPU: 1.023s

Dec 07 05:45:04 histfile systemd[1]: Started run-u36.service - /usr/bin/bash -c "dd if=/dev/zero bs=100M count=100 | tail > /dev/null".
Dec 07 05:45:05 histfile systemd[1]: run-u36.service: A process of this unit has been killed by the OOM killer.
Dec 07 05:45:05 histfile systemd[1]: run-u36.service: Failed with result 'oom-kill'.
Dec 07 05:45:05 histfile systemd[1]: run-u36.service: Consumed 1.023s CPU time, 500.0M memory peak, 0B memory swap peak.
```

