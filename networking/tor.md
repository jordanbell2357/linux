# Tor

## tor

<https://support.torproject.org/glossary/tor-tor-network-core-tor/>

> Tor is a program you can run on your computer that helps keep you safe on the Internet. It protects you by bouncing your communications around a
> distributed network of relays run by volunteers all around the world: it prevents somebody watching your Internet connection from learning what sites
> you visit, and it prevents the sites you visit from learning your physical location. This set of volunteer relays is called the Tor network.
> Sometimes the software associated with this network is called Core Tor, and sometimes "little-t tor".
> The way most people use Tor is with Tor Browser which is a version of Firefox that fixes many privacy issues.

<https://support.torproject.org/little-t-tor/>

<https://community.torproject.org/relay/setup/bridge/debian-ubuntu/>

<https://theinfopunk.com/posts/torsocks/>

```bash
sudo apt install tor
```

Enable tor daemon:

```bash
sudo systemctl enable --now tor
```

Check localhost with nmap:

```console
ubuntu@LAPTOP-JBell:~$ nmap localhost
Starting Nmap 7.80 ( https://nmap.org ) at 2025-10-18 19:57 EDT
Nmap scan report for localhost (127.0.0.1)
Host is up (0.000082s latency).
Not shown: 995 closed ports
PORT     STATE SERVICE
22/tcp   open  ssh
25/tcp   open  smtp
631/tcp  open  ipp
5432/tcp open  postgresql
9050/tcp open  tor-socks

Nmap done: 1 IP address (1 host up) scanned in 0.08 seconds
```

We're going to check our public IP address:

```console
curl 'https://api.ipify.org?format=json'
{"ip":"70.55.4.185"}
```

```console
ubuntu@LAPTOP-JBell:~$ curl https://check.torproject.org/api/ip
{"IsTor":false,"IP":"70.55.4.185"}
```

We use curl (<https://curl.se/docs/manpage.html#--socks5>) with the tor daemon:

```console
ubuntu@LAPTOP-JBell:~$ curl --socks5-hostname localhost:9050 https://check.torproject.org/api/ip
{"IsTor":true,"IP":"45.84.107.97"}
```

## torify

<https://linux.die.net/man/1/torify>

<https://justhackerthings.com/post/using-tor-from-the-command-line/>

```console
ubuntu@LAPTOP-JBell:~$ curl https://check.torproject.org/api/ip
{"IsTor":false,"IP":"70.55.4.185"}
```

```console
ubuntu@LAPTOP-JBell:~$ torify curl https://check.torproject.org/api/ip
{"IsTor":true,"IP":"45.84.107.97"}
```

<https://www.cia.gov/stories/story/cias-latest-layer-an-onion-site/>

> ciadotgov4sjwlzihbbgxnqg3xiyrg7so2r2o3lt5wz5ypk4sxyjstad.onion

```console
ubuntu@LAPTOP-JBell:~$ torify curl -s ciadotgov4sjwlzihbbgxnqg3xiyrg7so2r2o3lt5wz5ypk4sxyjstad.onion | html2text
<style type="text/css"> .no-show { display: none; } .disable-fade-in{ opacity:
1 !important; transform: none !important; visibility: visible !important; } </
style>
Skip_to_main_content
Contact
Contact
Report_InformationReport Information
[Agency_Logo]
Search CIA.govSearch
[query               ]
Today&#x27;s CIA
AboutLeadershipOrganizationMission_&_VisionPartner_with_CIATechnologyPrivacy
Careers
Career_OpportunitiesHiring_ProcessBenefitsAccommodationsVeteransStudent
Programs
Legacy
OriginHistoryMuseumHeadquartersTrailblazersIn_Memoriam
Newsroom
News_&_StoriesPress_Releases_&_StatementsSpeeches_&_TranscriptsThe_Langley
Files_Podcast
Library
ResourcesPublicationsPrepublication_ReviewStudy_of_IntelligenceWorld
FactbookCIA_ReportsCIA_MapsFOIA_Reading_Room
Contact CIAReport Information
****** We are
the Nation's
first line of
defense ******
We accomplish what others cannot accomplish and go where others cannot go
A career at CIA is unlike any other. We are looking for people from all
backgrounds and walks of life to carry out the work of a Nation.
Find_your_calling
[Headquarters Koi Pond][Headquarters Koi Pond]
[mission glyph][mission glyph]
***** Our Agency *****
We give U.S. leaders the intelligence they need to keep our country safe
As the world
```

## torsocks

```bash
sudo apt install torsocks
```

<https://gitlab.torproject.org/tpo/core/torsocks>

<https://support.torproject.org/glossary/torsocks/>

> Torsocks allows you to use many applications in a safer way with Tor. It ensures that DNS requests are handled safely and explicitly rejects any traffic other
> than TCP from the application you're using.

```console
ubuntu@LAPTOP-JBell:~$ torsocks curl https://check.torproject.org/api/ip
{"IsTor":true,"IP":"45.84.107.97"}
```

<https://theinfopunk.com/posts/torsocks/>

```console
ubuntu@LAPTOP-JBell:~$ torsocks curl wttr.in
Weather report: Amsterdam, Netherlands

                Overcast
       .--.     +10(9) °C
    .-(    ).   ← 12 km/h
   (___.__)__)  10 km
                0.0 mm
                                                       ┌─────────────┐                                                  
┌──────────────────────────────┬───────────────────────┤  Sat 18 Oct ├───────────────────────┬──────────────────────────────┐
│            Morning           │             Noon      └──────┬──────┘     Evening           │             Night            │
├──────────────────────────────┼──────────────────────────────┼──────────────────────────────┼──────────────────────────────┤
│     \   /     Sunny          │    \  /       Partly Cloudy  │               Overcast       │     \   /     Clear          │
│      .-.      +9(8) °C       │  _ /"".-.     +12(11) °C     │      .--.     +10(8) °C      │      .-.      +9(7) °C       │
│   ― (   ) ―   ← 11-16 km/h   │    \_(   ).   ← 11-14 km/h   │   .-(    ).   ← 12-21 km/h   │   ― (   ) ―   ← 12-20 km/h   │
│      `-’      10 km          │    /(___(__)  10 km          │  (___.__)__)  10 km          │      `-’      10 km          │
│     /   \     0.0 mm | 0%    │               0.0 mm | 0%    │               0.0 mm | 0%    │     /   \     0.0 mm | 0%    │
└──────────────────────────────┴──────────────────────────────┴──────────────────────────────┴──────────────────────────────┘
                                                       ┌─────────────┐                                                  
┌──────────────────────────────┬───────────────────────┤  Sun 19 Oct ├───────────────────────┬──────────────────────────────┐
│            Morning           │             Noon      └──────┬──────┘     Evening           │             Night            │
├──────────────────────────────┼──────────────────────────────┼──────────────────────────────┼──────────────────────────────┤
│    \  /       Partly Cloudy  │    \  /       Partly Cloudy  │  _`/"".-.     Patchy rain ne…│    \  /       Partly Cloudy  │
│  _ /"".-.     +9(7) °C       │  _ /"".-.     +13(12) °C     │   ,\_(   ).   +13(12) °C     │  _ /"".-.     +13(11) °C     │
│    \_(   ).   ↖ 14-20 km/h   │    \_(   ).   ↖ 16-20 km/h   │    /(___(__)  ↖ 13-24 km/h   │    \_(   ).   ↖ 17-28 km/h   │
│    /(___(__)  10 km          │    /(___(__)  10 km          │      ‘ ‘ ‘ ‘  10 km          │    /(___(__)  10 km          │
│               0.0 mm | 0%    │               0.0 mm | 0%    │     ‘ ‘ ‘ ‘   0.1 mm | 100%  │               0.0 mm | 0%    │
└──────────────────────────────┴──────────────────────────────┴──────────────────────────────┴──────────────────────────────┘
                                                       ┌─────────────┐                                                  
┌──────────────────────────────┬───────────────────────┤  Mon 20 Oct ├───────────────────────┬──────────────────────────────┐
│            Morning           │             Noon      └──────┬──────┘     Evening           │             Night            │
├──────────────────────────────┼──────────────────────────────┼──────────────────────────────┼──────────────────────────────┤
│               Cloudy         │  _`/"".-.     Patchy rain ne…│  _`/"".-.     Patchy rain ne…│  _`/"".-.     Patchy light d…│
│      .--.     +13(12) °C     │   ,\_(   ).   16 °C          │   ,\_(   ).   +14(12) °C     │   ,\_(   ).   +13(11) °C     │
│   .-(    ).   ↑ 18-25 km/h   │    /(___(__)  ↑ 21-27 km/h   │    /(___(__)  ↖ 18-30 km/h   │    /(___(__)  ↖ 20-31 km/h   │
│  (___.__)__)  10 km          │      ‘ ‘ ‘ ‘  10 km          │      ‘ ‘ ‘ ‘  10 km          │      ‘ ‘ ‘ ‘  5 km           │
│               0.0 mm | 0%    │     ‘ ‘ ‘ ‘   0.0 mm | 63%   │     ‘ ‘ ‘ ‘   0.0 mm | 66%   │     ‘ ‘ ‘ ‘   0.2 mm | 100%  │
└──────────────────────────────┴──────────────────────────────┴──────────────────────────────┴──────────────────────────────┘

Follow @igor_chubin for wttr.in updates
```

The terminal text is colored using ANSI escape sequences. We capture this using `aha` <https://github.com/theZiz/aha> and
<https://manpages.ubuntu.com/manpages/jammy/man1/aha.1.html>

```console
ubuntu@LAPTOP-JBell:~$ torify curl -s wttr.in/Toronto | aha --black > wttr.html
ubuntu@LAPTOP-JBell:~$ head wttr.html
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Strict//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-strict.dtd">
<!-- This file was created with the aha Ansi HTML Adapter. https://github.com/theZiz/aha -->
<html xmlns="http://www.w3.org/1999/xhtml">
<head>
<meta http-equiv="Content-Type" content="application/xml+xhtml; charset=UTF-8"/>
<title>stdin</title>
</head>
<body style="color:white; background-color:black">
<pre>
```

The HTML file `wttr.html` is here: <https://jordanbell.info/assets/html/wttr.html>
