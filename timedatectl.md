# timedatectl

<https://www.freedesktop.org/software/systemd/man/latest/timedatectl.html>

```console
ubuntu@jordanbell:~/weather$ sudo timedatectl status
               Local time: Thu 2025-12-04 01:04:53 UTC
           Universal time: Thu 2025-12-04 01:04:53 UTC
                 RTC time: Thu 2025-12-04 01:04:53
                Time zone: Etc/UTC (UTC, +0000)
System clock synchronized: yes
              NTP service: n/a
          RTC in local TZ: no
```

```console
ubuntu@jordanbell:~/weather$ sudo hwclock -v
hwclock from util-linux 2.39.3
System Time: 1764810338.144132
Trying to open: /dev/rtc0
Using the rtc interface to the clock.
Assuming hardware clock is kept in UTC time.
Waiting for clock tick...
...got clock tick
Time read from Hardware Clock: 2025/12/04 01:05:39
Hw clock time : 2025/12/04 01:05:39 = 1764810339 seconds since 1969
Time since last adjustment is 1764810339 seconds
Calculated Hardware Clock drift is 0.000000 seconds
2025-12-04 01:05:38.142678+00:00
```

```console
ubuntu@jordanbell:~/weather$ sudo hwclock --systohc
```

```console
ubuntu@jordanbell:~/weather$ sudo hwclock -v
hwclock from util-linux 2.39.3
System Time: 1764810453.474085
Trying to open: /dev/rtc0
Using the rtc interface to the clock.
Last drift adjustment done at 1764810449 seconds after 1969
Last calibration done at 1764810449 seconds after 1969
Hardware clock is on UTC time
Assuming hardware clock is kept in UTC time.
Waiting for clock tick...
...got clock tick
Time read from Hardware Clock: 2025/12/04 01:07:34
Hw clock time : 2025/12/04 01:07:34 = 1764810454 seconds since 1969
Time since last adjustment is 5 seconds
Calculated Hardware Clock drift is 0.000000 seconds
2025-12-04 01:07:33.472763+00:00
```
