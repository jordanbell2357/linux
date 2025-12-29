# date and time

## locale

https://man7.org/linux/man-pages/man1/locale.1.html

Running `locale -k LC_TIME` shows the keyword values for the locale category LC_TIME.

We inspect particular keywords

```console
$ locale -k d_fmt date_fmt
d_fmt="%m/%d/%y"
date_fmt="%a %b %e %H:%M:%S %Z %Y"
```

## /usr/share/zoneinfo

https://www.linuxjournal.com/content/add-your-city-linuxs-list-time-zones

```console
$ readlink /etc/localtime
/usr/share/zoneinfo/America/Toronto
```

```console
$ grep "America/Toronto" /usr/share/zoneinfo/zone.tab
CA      +4339-07923     America/Toronto Eastern - ON & QC (most areas)
```

```console
$ grep "Europe/Paris" /usr/share/zoneinfo/zone.tab
FR      +4852+00220     Europe/Paris
```

## zdump

https://man7.org/linux/man-pages/man8/zdump.8.html

```console
$ zdump UTC
UTC  Wed Dec 24 17:54:01 2025 UTC
$ zdump EST
EST  Wed Dec 24 12:53:58 2025 EST
$ zdump America/Toronto
America/Toronto  Wed Dec 24 12:54:13 2025 EST
```

> -c [loyear,]hiyear Cut off interval output at the given year(s).

```console
$ zdump -v -c 2026,2027 America/New_York
America/New_York  Sun Mar  8 06:59:59 2026 UT = Sun Mar  8 01:59:59 2026 EST isdst=0 gmtoff=-18000
America/New_York  Sun Mar  8 07:00:00 2026 UT = Sun Mar  8 03:00:00 2026 EDT isdst=1 gmtoff=-14400
America/New_York  Sun Nov  1 05:59:59 2026 UT = Sun Nov  1 01:59:59 2026 EDT isdst=1 gmtoff=-14400
America/New_York  Sun Nov  1 06:00:00 2026 UT = Sun Nov  1 01:00:00 2026 EST isdst=0 gmtoff=-18000
```

The values of gmtoff is the UTC offset in seconds. -18000 seconds is -5 hours, and -14400 seconds is -4 hours.
We see from the above when the transitions between EST and EDT happen, and that the UTC offset is -0500 hours during EST
and -0400 hours during EDT.


## tzselect

https://www.man7.org/linux/man-pages/man8/tzselect.8.html

> -c coord Instead of asking for continent and then country and then city, ask for selection from time zones whose largest cities are closest to the location with geographical coordinates coord.  Use ISO 6709 notation for coord, that is, a latitude immediately followed by a longitude.  The latitude and longitude should be signed integers followed by an optional decimal point and fraction: positive numbers represent north and east, negative south and west. Latitudes with two and longitudes with three integer digits are treated as degrees; latitudes with four or six and longitudes with five or seven integer digits are treated as DDMM, DDDMM, DDMMSS, or DDDMMSS representing DD or DDD degrees, MM minutes, and zero or SS seconds, with any trailing fractions represent fractional minutes or (if SS is present) seconds.  The decimal point is that of the current locale.  For example, in the (default) C locale, -c +40.689-074.045 specifies 40.689 degrees N, 74.045 degrees W, -c +4041.4-07402.7 specifies 40 degrees 41.4 minutes N, 74 degrees 2.7 minutes W, and -c +404121-0740240 specifies 40 degrees 41 minutes 21 seconds N, 74 degrees 2 minutes 40 seconds W.  If coord is not one of the documented forms, the resulting behavior is unspecified.

```console
$ tzselect -c +485124+0022108 -n 1
Please identify a location so that time zone rules can be set correctly.
Please select one of the following timezones, echo listed roughly in increasing order of distance from +485124+0022108.
1) France, Monaco
#? 1

The following information has been given:

        coord +485124+0022108
        France, Monaco

Therefore TZ='Europe/Paris' will be used.
Selected time is now:   Thu Dec 25 01:02:49 CET 2025.
Universal Time is now:  Thu Dec 25 00:02:49 UTC 2025.
Is the above information OK?
1) Yes
2) No
#? 1

You can make this change permanent for yourself by appending the line
        TZ='Europe/Paris'; export TZ
to the file '.profile' in your home directory; then log out and log in again.

Here is that TZ value again, this time on standard output so that you
can use the /usr/bin/tzselect command in shell scripts:
Europe/Paris
```

## timedatectl

https://www.freedesktop.org/software/systemd/man/latest/timedatectl.html

https://www.freedesktop.org/software/systemd/man/latest/systemd-timesyncd.service.html

https://opensource.com/article/20/6/time-date-systemd

Using systemd-timesyncd (`sudo apt install systemd-timesyncd`):

```console
$ timedatectl
               Local time: Wed 2025-12-24 21:53:15 EST
           Universal time: Thu 2025-12-25 02:53:15 UTC
                 RTC time: Thu 2025-12-25 02:53:14
                Time zone: America/Toronto (EST, -0500)
System clock synchronized: yes
              NTP service: active
          RTC in local TZ: no
```

Using NTPSec (`sudo apt install ntpsec`):

```console
$ timedatectl timesync-status
       Server: 185.125.190.57 (ntp.ubuntu.com)
Poll interval: 32s (min: 32s; max 34min 8s)
         Leap: normal
      Version: 4
      Stratum: 2
    Reference: C279CFF9
    Precision: 1us (-25)
Root distance: 930us (max: 5s)
       Offset: +2.681119s
        Delay: 87.270ms
       Jitter: 2.091480s
 Packet count: 3
    Frequency: +7.135ppm
```

## ntpdig

https://docs.ntpsec.org/latest/ntpdig.html

```console
$ ntpdig pool.ntp.org
2025-12-24 21:55:01.778821 (-0500) +0.981645 +/- 0.025685 pool.ntp.org 51.222.12.92 s2 no-leap
$ ntpdig time.aws.com
2025-12-24 21:57:46.970247 (-0500) +0.489557 +/- 0.011591 time.aws.com 3.86.4.106 s4 no-leap
```

## date

https://man7.org/linux/man-pages/man1/date.1.html

https://pubs.opengroup.org/onlinepubs/009695399/utilities/date.html

> %u   day of week (1..7); 1 is Monday

```console
$ date --date 'Sunday' '+%u'
7
```

> %V     ISO week number, with Monday as first day of week (01..53)

> %G     year of ISO week number; normally useful only with %V

```console
$ date '+%V/%G'
52/2025
```

> %A     locale's full weekday name (e.g., Sunday)

```console
$ date -d "1974-01-04" +"%A"
Friday
```

> -I[FMT], --iso-8601[=FMT] 
>              output date/time in ISO 8601 format.  FMT='date' for date
>              only (the default), 'hours', 'minutes', 'seconds', or 'ns'
>              for date and time to the indicated precision.

```console
$ date --iso-8601="second"
2025-12-24T17:51:27-05:00
$ date -I"second"
2025-12-24T17:51:30-05:00
```

```console
$ TZ=MST date --date 'March 1, 2015 +12 days +12 hours +15 minutes'
Fri Mar 13 12:15:00 MST 2015
```

https://www.pixelbeat.org/docs/linux_timezones/

```console
$ date -u
Thu Dec 25 03:12:18 UTC 2025
$ TZ="America/Phoenix" date -R --date='TZ="Europe/Dublin" 19:00 tomorrow'
Fri, 26 Dec 2025 12:00:00 -0700
```

## cal

https://man7.org/linux/man-pages/man1/cal.1.html

```console
$ cal
   December 2025
Su Mo Tu We Th Fr Sa
    1  2  3  4  5  6
 7  8  9 10 11 12 13
14 15 16 17 18 19 20
21 22 23 24 25 26 27
28 29 30 31
```

