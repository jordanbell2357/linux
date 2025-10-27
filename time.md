# time

<https://ss64.com/bash/time.html>

<https://tldp.org/LDP/GNU-Linux-Tools-Summary/html/c4268.htm>

```console
ubuntu@LAPTOP-JBell:~$ /usr/bin/time -v dd if=/dev/random bs=100M count=1 status=none | tail > /dev/null
        Command being timed: "dd if=/dev/random bs=100M count=1 status=none"
        User time (seconds): 0.00
        System time (seconds): 0.25
        Percent of CPU this job got: 94%
        Elapsed (wall clock) time (h:mm:ss or m:ss): 0:00.27
        Average shared text size (kbytes): 0
        Average unshared data size (kbytes): 0
        Average stack size (kbytes): 0
        Average total size (kbytes): 0
        Maximum resident set size (kbytes): 104192
        Average resident set size (kbytes): 0
        Major (requiring I/O) page faults: 0
        Minor (reclaiming a frame) page faults: 25708
        Voluntary context switches: 4357
        Involuntary context switches: 9
        Swaps: 0
        File system inputs: 0
        File system outputs: 0
        Socket messages sent: 0
        Socket messages received: 0
        Signals delivered: 0
        Page size (bytes): 4096
        Exit status: 0
```
