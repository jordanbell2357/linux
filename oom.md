# oom

<https://stackoverflow.com/a/34755981/11683596>

## Clearing logs

dmesg:

```console
ubuntu@LAPTOP-JBell:~$ sudo dmesg -C
```

kern.log or syslog:

```console
ubuntu@LAPTOP-JBell:~$ sudo truncate -s 0 /var/log/kern.log
```

journalctl:

```console
ubuntu@LAPTOP-JBell:~$ sudo journalctl --rotate  
ubuntu@LAPTOP-JBell:~$ sudo journalctl -q --vacuum-time=1s
```

## Causing OOM Killer

Checking available memory:

```console
ubuntu@LAPTOP-JBell:~$ vmstat --unit M -s | head
         7802 M total memory
          631 M used memory
           91 M active memory
          160 M inactive memory
         7019 M free memory
           16 M buffer memory
          134 M swap cache
         2048 M total swap
          480 M used swap
         1567 M free swap
```

Forcing out of memory killer:

```
ubuntu@LAPTOP-JBell:~$ echo $(date); head -c 10G /dev/zero | pv -L 1G | tail > /dev/null; echo $?
Thu Oct 23 23:13:47 EDT 2025
8.44GiB 0:00:11 [ 754MiB/s] [                    <=>                                                                   ]
Killed
137
```

## Viewing logs

dmesg:

```console
ubuntu@LAPTOP-JBell:~$ sudo dmesg -H -k -P -T | tail
[Thu Oct 23 23:16:06 2025] [  25700]     0 25700      772       96    45056        0             0 Relay(16980)
[Thu Oct 23 23:16:06 2025] [  25702]  1000 25702     1628      288    61440      416             0 bash
[Thu Oct 23 23:16:06 2025] [  29410]     0 29410      772       96    45056        0             0 SessionLeader
[Thu Oct 23 23:16:06 2025] [  29412]     0 29412      772       96    45056        0             0 Relay(19503)
[Thu Oct 23 23:16:06 2025] [  29414]  1000 29414     1562      160    65536      448             0 bash
[Thu Oct 23 23:16:06 2025] [  31948]  1000 31948      807      160    49152        0             0 head
[Thu Oct 23 23:16:06 2025] [  31949]  1000 31949      844      192    53248       32             0 pv
[Thu Oct 23 23:16:06 2025] [  31950]  1000 31950  2223088  1822336 17866752   399936             0 tail
[Thu Oct 23 23:16:06 2025] oom-kill:constraint=CONSTRAINT_NONE,nodemask=(null),cpuset=/,mems_allowed=0,global_oom,task_memcg=/,task=tail,pid=31950,uid=1000
[Thu Oct 23 23:16:06 2025] Out of memory: Killed process 31950 (tail) total-vm:8892352kB, anon-rss:7288704kB, file-rss:640kB, shmem-rss:0kB, UID:1000 pgtables:17448kB oom_score_adj:0
```

We note the difference in the local times reported by dmesg on the one hand, and kern.log and journalctl on the other hand.

kern.log or syslog:

```console
ubuntu@LAPTOP-JBell:~$ cat /var/log/kern.log | grep -E -i 'memory|oom'
Oct 23 23:13:58 LAPTOP-JBell kernel: [111764.566248] pv invoked oom-killer: gfp_mask=0x140cca(GFP_HIGHUSER_MOVABLE|__GFP_COMP), order=0, oom_score_adj=0
Oct 23 23:13:58 LAPTOP-JBell kernel: [111764.566404]  oom_kill_process+0x100/0x1a0
Oct 23 23:13:58 LAPTOP-JBell kernel: [111764.566407]  out_of_memory+0x11d/0x560
Oct 23 23:13:58 LAPTOP-JBell kernel: [111764.566765] Tasks state (memory values in pages):
Oct 23 23:13:58 LAPTOP-JBell kernel: [111764.566765] [  pid  ]   uid  tgid total_vm      rss pgtables_bytes swapents oo_score_adj name
Oct 23 23:13:58 LAPTOP-JBell kernel: [111764.567193] oom-kill:constraint=CONSTRAINT_NONE,nodemask=(null),cpuset=/,mems_allowed=0,global_oom,task_memcg=/,task=tail,pid=31950,uid=1000
Oct 23 23:13:58 LAPTOP-JBell kernel: [111764.567223] Out of memory: Killed process 31950 (tail) total-vm:8892352kB, anon-rss:7288704kB, file-rss:640kB, shmem-rss:0kB, UID:1000 pgtables:17448kB oom_score_adj:0
```

journalctl:

```console
ubuntu@LAPTOP-JBell:~$ journalctl -g memory -k -o short-full --no-pager
Thu 2025-10-23 23:13:58 EDT LAPTOP-JBell kernel:  out_of_memory+0x11d/0x560
Thu 2025-10-23 23:13:58 EDT LAPTOP-JBell kernel: Tasks state (memory values in pages):
Thu 2025-10-23 23:13:58 EDT LAPTOP-JBell kernel: Out of memory: Killed process 31950 (tail) total-vm:8892352kB, anon-rss:7288704kB, file-rss:640kB, shmem-rss:0kB, UID:1000 pgtables:17448kB oom_score_adj:0
```

