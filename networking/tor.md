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


<body style="color:white; background-color:black">
<pre>
Weather report: Toronto

  <span style="color:#ffff00;">   \  /</span>       Partly cloudy
  <span style="color:#ffff00;"> _ /&quot;&quot;</span><span style="color:#c0c0c0;">.-.    </span> <span style="color:#afff00;">18</span> °C
  <span style="color:#ffff00;">   \_</span><span style="color:#c0c0c0;">(   ).  </span> <span style="font-weight:bold;">↑</span> <span style="color:#ffff00;">13</span> km/h
  <span style="color:#ffff00;">   /</span><span style="color:#c0c0c0;">(___(__) </span> 14 km
                0.0 mm
                                                       ┌─────────────┐                                                  
┌──────────────────────────────┬───────────────────────┤  Sat 18 Oct ├───────────────────────┬──────────────────────────────┐
│            Morning           │             Noon      └──────┬──────┘     Evening           │             Night            │
├──────────────────────────────┼──────────────────────────────┼──────────────────────────────┼──────────────────────────────┤
│ <span style="color:#ffff00;">    \   /    </span> Sunny          │ <span style="color:#ffff00;">    \   /    </span> Sunny          │ <span style="color:#ffff00;">    \   /    </span> Sunny          │ <span style="color:#ffff00;">    \   /    </span> Clear          │
│ <span style="color:#ffff00;">     .-.     </span> <span style="color:#87ff00;">14</span> °C          │ <span style="color:#ffff00;">     .-.     </span> <span style="color:#afff00;">18</span> °C          │ <span style="color:#ffff00;">     .-.     </span> <span style="color:#d7ff00;">21</span> °C          │ <span style="color:#ffff00;">     .-.     </span> <span style="color:#afff00;">16</span> °C          │
│ <span style="color:#ffff00;">  ― (   ) ―  </span> <span style="font-weight:bold;">↑</span> <span style="color:#d7ff00;">11</span>-<span style="color:#ffd700;">17</span> km/h   │ <span style="color:#ffff00;">  ― (   ) ―  </span> <span style="font-weight:bold;">↑</span> <span style="color:#ffd700;">18</span>-<span style="color:#ffaf00;">23</span> km/h   │ <span style="color:#ffff00;">  ― (   ) ―  </span> <span style="font-weight:bold;">↑</span> <span style="color:#ffff00;">14</span>-<span style="color:#ff8700;">27</span> km/h   │ <span style="color:#ffff00;">  ― (   ) ―  </span> <span style="font-weight:bold;">↖</span> <span style="color:#ffff00;">13</span>-<span style="color:#ff8700;">25</span> km/h   │
│ <span style="color:#ffff00;">     `-’     </span> 10 km          │ <span style="color:#ffff00;">     `-’     </span> 10 km          │ <span style="color:#ffff00;">     `-’     </span> 10 km          │ <span style="color:#ffff00;">     `-’     </span> 10 km          │
│ <span style="color:#ffff00;">    /   \    </span> 0.0 mm | 0%    │ <span style="color:#ffff00;">    /   \    </span> 0.0 mm | 0%    │ <span style="color:#ffff00;">    /   \    </span> 0.0 mm | 0%    │ <span style="color:#ffff00;">    /   \    </span> 0.0 mm | 0%    │
└──────────────────────────────┴──────────────────────────────┴──────────────────────────────┴──────────────────────────────┘
                                                       ┌─────────────┐                                                  
┌──────────────────────────────┬───────────────────────┤  Sun 19 Oct ├───────────────────────┬──────────────────────────────┐
│            Morning           │             Noon      └──────┬──────┘     Evening           │             Night            │
├──────────────────────────────┼──────────────────────────────┼──────────────────────────────┼──────────────────────────────┤
│ <span style="color:#ffff00;">    \   /    </span> Sunny          │ <span style="color:#ffff00;">   \  /</span>       Partly Cloudy  │               Overcast       │               Overcast       │
│ <span style="color:#ffff00;">     .-.     </span> <span style="color:#afff00;">17</span> °C          │ <span style="color:#ffff00;"> _ /&quot;&quot;</span><span style="color:#c0c0c0;">.-.    </span> <span style="color:#d7ff00;">20</span> °C          │ <span style="font-weight:bold;color:#555555;">     .--.    </span> <span style="color:#afff00;">17</span> °C          │ <span style="font-weight:bold;color:#555555;">     .--.    </span> <span style="color:#87ff00;">+14</span>(<span style="color:#5fff00;">12</span>) °C     │
│ <span style="color:#ffff00;">  ― (   ) ―  </span> <span style="font-weight:bold;">↖</span> <span style="color:#ffaf00;">23</span>-<span style="color:#ff0000;">42</span> km/h   │ <span style="color:#ffff00;">   \_</span><span style="color:#c0c0c0;">(   ).  </span> <span style="font-weight:bold;">↑</span> <span style="color:#ff8700;">27</span>-<span style="color:#ff0000;">44</span> km/h   │ <span style="font-weight:bold;color:#555555;">  .-(    ).  </span> <span style="font-weight:bold;">↗</span> <span style="color:#ff5f00;">29</span>-<span style="color:#ff0000;">40</span> km/h   │ <span style="font-weight:bold;color:#555555;">  .-(    ).  </span> <span style="font-weight:bold;">→</span> <span style="color:#ffd700;">18</span>-<span style="color:#ff8700;">24</span> km/h   │
│ <span style="color:#ffff00;">     `-’     </span> 9 km           │ <span style="color:#ffff00;">   /</span><span style="color:#c0c0c0;">(___(__) </span> 10 km          │ <span style="font-weight:bold;color:#555555;"> (___.__)__) </span> 2 km           │ <span style="font-weight:bold;color:#555555;"> (___.__)__) </span> 10 km          │
│ <span style="color:#ffff00;">    /   \    </span> 0.0 mm | 0%    │               0.0 mm | 0%    │               0.0 mm | 0%    │               0.0 mm | 0%    │
└──────────────────────────────┴──────────────────────────────┴──────────────────────────────┴──────────────────────────────┘
                                                       ┌─────────────┐                                                  
┌──────────────────────────────┬───────────────────────┤  Mon 20 Oct ├───────────────────────┬──────────────────────────────┐
│            Morning           │             Noon      └──────┬──────┘     Evening           │             Night            │
├──────────────────────────────┼──────────────────────────────┼──────────────────────────────┼──────────────────────────────┤
│               Overcast       │ <span style="color:#ffff00;">    \   /    </span> Sunny          │ <span style="color:#ffff00;">    \   /    </span> Sunny          │ <span style="color:#ffff00;">    \   /    </span> Clear          │
│ <span style="font-weight:bold;color:#555555;">     .--.    </span> <span style="color:#5fff00;">+12</span>(<span style="color:#00ff00;">9</span>) °C      │ <span style="color:#ffff00;">     .-.     </span> <span style="color:#87ff00;">+14</span>(<span style="color:#87ff00;">13</span>) °C     │ <span style="color:#ffff00;">     .-.     </span> <span style="color:#5fff00;">+12</span>(<span style="color:#5fff00;">10</span>) °C     │ <span style="color:#ffff00;">     .-.     </span> <span style="color:#5fff00;">+10</span>(<span style="color:#00ff5f;">7</span>) °C      │
│ <span style="font-weight:bold;color:#555555;">  .-(    ).  </span> <span style="font-weight:bold;">→</span> <span style="color:#ffaf00;">20</span>-<span style="color:#ff8700;">26</span> km/h   │ <span style="color:#ffff00;">  ― (   ) ―  </span> <span style="font-weight:bold;">↘</span> <span style="color:#ffaf00;">22</span>-<span style="color:#ff8700;">26</span> km/h   │ <span style="color:#ffff00;">  ― (   ) ―  </span> <span style="font-weight:bold;">↘</span> <span style="color:#ffff00;">15</span>-<span style="color:#ffaf00;">21</span> km/h   │ <span style="color:#ffff00;">  ― (   ) ―  </span> <span style="font-weight:bold;">↘</span> <span style="color:#afff00;">9</span>-<span style="color:#ffff00;">13</span> km/h    │
│ <span style="font-weight:bold;color:#555555;"> (___.__)__) </span> 10 km          │ <span style="color:#ffff00;">     `-’     </span> 10 km          │ <span style="color:#ffff00;">     `-’     </span> 10 km          │ <span style="color:#ffff00;">     `-’     </span> 10 km          │
│               0.0 mm | 0%    │ <span style="color:#ffff00;">    /   \    </span> 0.0 mm | 0%    │ <span style="color:#ffff00;">    /   \    </span> 0.0 mm | 0%    │ <span style="color:#ffff00;">    /   \    </span> 0.0 mm | 0%    │
└──────────────────────────────┴──────────────────────────────┴──────────────────────────────┴──────────────────────────────┘
Location: Toronto, Ontario, Canada [43.6529206,-79.3849007]

Follow <span style="background-color:aqua;"></span><span style="color:dimgray;background-color:aqua;">@igor_chubin</span> for wttr.in updates
</pre>
</body>

