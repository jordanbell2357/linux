# sar

<https://www.linuxjournal.com/content/how-use-sar-system-activity-reporter>

<https://man7.org/linux/man-pages/man1/sar.1.html>

In one terminal:

```console
ubuntu@LAPTOP-JBell:~$ sar -h -r 1 15
Linux 6.6.87.2-microsoft-standard-WSL2 (LAPTOP-JBell)   10/25/25        _x86_64_        (16 CPU)

22:37:02    kbmemfree   kbavail kbmemused  %memused kbbuffers  kbcached  kbcommit   %commit  kbactive   kbinact   kbdirty
22:37:03         6.7G      6.7G    680.4M      8.7%      6.7M     69.2M      2.6G     27.2%     44.3M    410.9M    188.0k
22:37:04         5.8G      5.7G      1.7G     21.7%      6.7M     70.8M      3.6G     37.5%     44.4M      1.4G    192.0k
22:37:05         4.8G      4.7G      2.7G     34.8%      6.7M     70.9M      4.6G     47.8%     44.4M      2.4G    192.0k
22:37:06         3.7G      3.7G      3.7G     48.2%      6.7M     70.9M      5.6G     58.4%     44.4M      3.4G    192.0k
22:37:07         2.7G      2.7G      4.7G     61.2%      6.7M     70.9M      6.6G     68.6%     44.4M      4.4G    192.0k
22:37:08         1.7G      1.7G      5.7G     74.4%      6.7M     70.9M      7.6G     79.1%     44.4M      5.4G    192.0k
22:37:09       770.9M    744.5M      6.7G     87.4%      6.7M     70.9M      8.6G     89.3%     44.4M      6.4G    188.0k
22:37:10        60.4M      2.0M      7.4G     97.3%    820.0k     12.3M      9.4G     97.4%     26.9M      7.1G    172.0k
22:37:11        67.6M     16.7M      7.4G     97.0%      2.0M     27.1M     10.3G    107.0%     38.7M      7.1G      0.0k
22:37:12        59.5M      0.0k      7.4G     97.4%      1.3M      8.7M     11.0G    114.2%    632.4M      6.5G      0.0k
22:37:13         7.1G      7.1G    354.6M      4.5%      5.1M     44.3M      2.3G     24.1%     56.9M     49.7M      1.1M
22:37:14         7.1G      7.1G    354.8M      4.5%      5.1M     45.1M      2.3G     24.1%     57.0M     50.4M      1.1M
22:37:15         7.0G      6.9G    483.3M      6.2%      5.8M     49.3M      2.3G     24.1%     60.8M     51.2M      1.1M
22:37:16         7.1G      7.0G    355.3M      4.6%      5.8M     49.3M      2.3G     24.1%     60.8M     51.2M      1.1M
22:37:17         7.1G      7.0G    355.4M      4.6%      5.8M     49.9M      2.3G     24.1%     61.5M     51.6M      1.1M
Average:         4.1G      4.1G      3.3G     43.5%      5.2M     52.0M      5.4G     56.4%     87.0M      3.0G    477.3k
```

In another:

```bash
ubuntu@LAPTOP-JBell:~$ head -c 10G /dev/zero | pv -L 1G | tail > /dev/null
8.63GiB 0:00:09 [ 901MiB/s] [                 <=>                                                                      ]
Killed
ubuntu@LAPTOP-JBell:~$ echo $?
137
```

