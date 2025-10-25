# CPU Monitoring Linux

## /proc/cpuinfo

```console
ubuntu@LAPTOP-JBell:~$ head -n 13 /proc/cpuinfo
processor       : 0
vendor_id       : GenuineIntel
cpu family      : 6
model           : 141
model name      : 11th Gen Intel(R) Core(TM) i7-11800H @ 2.30GHz
stepping        : 1
microcode       : 0xffffffff
cpu MHz         : 2304.008
cache size      : 24576 KB
physical id     : 0
siblings        : 16
core id         : 0
cpu cores       : 8
```

## lscpu

```console
ubuntu@LAPTOP-JBell:~$ lscpu | head -n 15
Architecture:                         x86_64
CPU op-mode(s):                       32-bit, 64-bit
Address sizes:                        39 bits physical, 48 bits virtual
Byte Order:                           Little Endian
CPU(s):                               16
On-line CPU(s) list:                  0-15
Vendor ID:                            GenuineIntel
Model name:                           11th Gen Intel(R) Core(TM) i7-11800H @ 2.30GHz
CPU family:                           6
Model:                                141
Thread(s) per core:                   2
Core(s) per socket:                   8
Socket(s):                            1
Stepping:                             1
BogoMIPS:                             4608.01
```

## getconf

```console
ubuntu@LAPTOP-JBell:~$ getconf _NPROCESSORS_ONLN
16
```

## nproc

```console
ubuntu@LAPTOP-JBell:~$ nproc
16
```

## sar

```console
ubuntu@LAPTOP-JBell:~$ sar -u 1 5
Linux 6.6.87.2-microsoft-standard-WSL2 (LAPTOP-JBell)   10/13/25        _x86_64_        (16 CPU)

16:26:52        CPU     %user     %nice   %system   %iowait    %steal     %idle
16:26:55        all      0.06      0.00      0.25      0.00      0.00     99.69
16:26:56        all      0.19      0.00      0.19      0.00      0.00     99.63
16:26:57        all      0.00      0.00      0.12      0.00      0.00     99.88
16:26:58        all      0.19      0.00      0.00      0.00      0.00     99.81
16:26:59        all      0.06      0.00      0.19      0.00      0.00     99.75
Average:        all      0.10      0.00      0.15      0.00      0.00     99.75
```

For logs of sar:

```bash
sudo dpkg-reconfigure sysstat
```

is equivalent to editing `/etc/default/sysstat` and changing ENABLED="false" to ENABLED="true" and executing

```bash
systemctl restart sysstat.service
```

## yes

<https://linuxconfig.org/how-to-stress-test-your-cpu-on-linux>

```console
ubuntu@LAPTOP-JBell:~$ for i in $(seq $(getconf _NPROCESSORS_ONLN)); do yes > /dev/null & done
[1] 6208
[2] 6209
[3] 6210
[4] 6211
[5] 6212
[6] 6213
[7] 6214
[8] 6215
[9] 6216
[10] 6217
[11] 6218
[12] 6219
[13] 6220
[14] 6221
[15] 6222
[16] 6223
ubuntu@LAPTOP-JBell:~$ killall yes
[1]   Terminated              yes > /dev/null
[2]   Terminated              yes > /dev/null
[3]   Terminated              yes > /dev/null
[4]   Terminated              yes > /dev/null
[5]   Terminated              yes > /dev/null
[6]   Terminated              yes > /dev/null
[7]   Terminated              yes > /dev/null
[8]   Terminated              yes > /dev/null
[9]   Terminated              yes > /dev/null
[10]   Terminated              yes > /dev/null
[11]   Terminated              yes > /dev/null
[12]   Terminated              yes > /dev/null
[13]   Terminated              yes > /dev/null
[14]   Terminated              yes > /dev/null
[15]-  Terminated              yes > /dev/null
[16]+  Terminated              yes > /dev/null
```

```console
ubuntu@LAPTOP-JBell:~$ sar -u 1
Linux 6.6.87.2-microsoft-standard-WSL2 (LAPTOP-JBell)   10/13/25        _x86_64_        (16 CPU)

16:38:20        CPU     %user     %nice   %system   %iowait    %steal     %idle
16:38:21        all      0.13      0.00      0.06      0.00      0.00     99.81
16:38:22        all      0.06      0.00      0.25      0.00      0.00     99.69
16:38:23        all      1.93      0.00      5.04      0.00      0.00     93.03
16:38:24        all     31.14      0.00     68.86      0.00      0.00      0.00
16:38:25        all     28.96      0.00     71.04      0.00      0.00      0.00
16:38:26        all     29.24      0.00     70.76      0.00      0.00      0.00
16:38:27        all     31.13      0.00     68.87      0.00      0.00      0.00
16:38:28        all     19.56      0.00     48.19      0.00      0.00     32.25
16:38:29        all      0.00      0.00      0.12      0.00      0.00     99.88
16:38:30        all      0.06      0.00      0.19      0.00      0.00     99.75
16:38:31        all      0.13      0.00      0.19      0.00      0.00     99.69
^C

Average:        all     12.94      0.00     30.32      0.00      0.00     56.74
```

## perf

<https://perfwiki.github.io/main/>

<https://www.brendangregg.com/perf.html>
