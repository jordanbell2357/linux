# date and time

## date

https://www.linuxjournal.com/content/doing-date-math-command-line-part-i

`%u   day of week (1..7); 1 is Monday`

```console
$ date --date 'Sunday' '+%u'
7
```

```console
$ date +"Week number: %V Year: %y"
Week number: 52 Year: 25
$ date +%V/%G # ISO week number/Year of ISO week number
52/2025
$ date -d "1974-01-04" +"%A"
Friday
$ date --iso-8601="second"
2025-12-24T16:43:38-05:00
$ TZ=MST date --date 'March 1, 2015 +12 days +12 hours +15 minutes'
Fri Mar 13 12:15:00 MST 2015

```

## zdump

```console
$ zdump UTC
UTC  Wed Dec 24 17:54:01 2025 UTC
$ zdump EST
EST  Wed Dec 24 12:53:58 2025 EST
$ zdump America/Toronto
America/Toronto  Wed Dec 24 12:54:13 2025 EST
```


## cal

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

