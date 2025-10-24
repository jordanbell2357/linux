# stress-ng

<https://www.mankier.com/1/stress-ng>

<https://wiki.ubuntu.com/Kernel/Reference/stress-ng>

```console
ubuntu@LAPTOP-JBell:~$ sudo dmesg -C
ubuntu@LAPTOP-JBell:~$ sudo stress-ng --metrics-brief --oomable --timeout=30s --brk 1
stress-ng: info:  [27959] setting to a 30 second run per stressor
stress-ng: info:  [27959] dispatching hogs: 1 brk
stress-ng: info:  [27959] successful run completed in 13.87s
stress-ng: info:  [27959] stressor       bogo ops real time  usr time  sys time   bogo ops/s     bogo ops/s
stress-ng: info:  [27959]                           (secs)    (secs)    (secs)   (real time) (usr+sys time)
stress-ng: info:  [27959] brk             3978295     13.87      1.06     12.74    286927.49      288282.25
ubuntu@LAPTOP-JBell:~$ sudo dmesg | grep "Out of memory"
[117312.487945] Out of memory: Killed process 41835 (stress-ng) total-vm:12441152kB, anon-rss:7096516kB, file-rss:128kB, shmem-rss:0kB, UID:0 pgtables:17136kB oom_score_adj:1000
```

```console
ubuntu@LAPTOP-JBell:~$ sudo stress-ng --metrics-brief --oomable --timeout=30s --vm 2 --vm-bytes 10g
stress-ng: info:  [28340] setting to a 30 second run per stressor
stress-ng: info:  [28340] dispatching hogs: 2 vm
stress-ng: info:  [28340] successful run completed in 30.17s
stress-ng: info:  [28340] stressor       bogo ops real time  usr time  sys time   bogo ops/s     bogo ops/s
stress-ng: info:  [28340]                           (secs)    (secs)    (secs)   (real time) (usr+sys time)
stress-ng: info:  [28340] vm               563619     17.44      8.63     16.87     32316.88       22102.71
ubuntu@LAPTOP-JBell:~$ sudo dmesg | grep "Out of memory"
[117586.586496] Out of memory: Killed process 42375 (stress-ng) total-vm:5307120kB, anon-rss:3679456kB, file-rss:384kB, shmem-rss:0kB, UID:0 pgtables:10348kB oom_score_adj:1000
```

```console
ubuntu@LAPTOP-JBell:~$ sudo stress-ng --metrics-brief --oomable --timeout=30s --bigheap 10 --bigheap-growth 64m
stress-ng: info:  [28531] setting to a 30 second run per stressor
stress-ng: info:  [28531] dispatching hogs: 10 bigheap
stress-ng: info:  [28531] successful run completed in 30.32s
stress-ng: info:  [28531] stressor       bogo ops real time  usr time  sys time   bogo ops/s     bogo ops/s
stress-ng: info:  [28531]                           (secs)    (secs)    (secs)   (real time) (usr+sys time)
stress-ng: info:  [28531] bigheap             272     18.05      2.05     41.96        15.07           6.18
ubuntu@LAPTOP-JBell:~$ sudo dmesg | grep "Out of memory"
[117704.764525] Out of memory: Killed process 42629 (stress-ng) total-vm:1047300kB, anon-rss:788704kB, file-rss:640kB, shmem-rss:0kB, UID:0 pgtables:1948kB oom_score_adj:1000
[117705.281330] Out of memory: Killed process 42635 (stress-ng) total-vm:1112836kB, anon-rss:808544kB, file-rss:768kB, shmem-rss:0kB, UID:0 pgtables:2028kB oom_score_adj:1000
[117712.857472] Out of memory: Killed process 42642 (stress-ng) total-vm:1768196kB, anon-rss:1530592kB, file-rss:384kB, shmem-rss:0kB, UID:0 pgtables:3328kB oom_score_adj:1000
[117713.965227] Out of memory: Killed process 42637 (stress-ng) total-vm:2161412kB, anon-rss:1910368kB, file-rss:256kB, shmem-rss:0kB, UID:0 pgtables:4080kB oom_score_adj:1000
[117716.788528] Out of memory: Killed process 42630 (stress-ng) total-vm:2161412kB, anon-rss:1924832kB, file-rss:896kB, shmem-rss:0kB, UID:0 pgtables:4080kB oom_score_adj:1000
[117717.952763] Out of memory: Killed process 42639 (stress-ng) total-vm:2161412kB, anon-rss:1702624kB, file-rss:768kB, shmem-rss:0kB, UID:0 pgtables:4080kB oom_score_adj:1000
```
