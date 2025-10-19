# VMware Workstation Pro

<https://support.broadcom.com/group/ecx/free-downloads>






# IPv6

<https://curl.se/docs/tutorial.html>

```console
ubuntu@LAPTOP-JBell:~$ nslookup -query=AAAA ipv6.google.com
Server:         10.255.255.254
Address:        10.255.255.254#53

Non-authoritative answer:
ipv6.google.com canonical name = ipv6.l.google.com.
Name:   ipv6.l.google.com
Address: 2607:f8b0:400b:807::200e
```

```console
ubuntu@LAPTOP-JBell:~$ dig AAAA ipv6.google.com

; <<>> DiG 9.18.39-0ubuntu0.22.04.1-Ubuntu <<>> AAAA ipv6.google.com
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 38857
;; flags: qr rd ra; QUERY: 1, ANSWER: 2, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 1232
;; QUESTION SECTION:
;ipv6.google.com.               IN      AAAA

;; ANSWER SECTION:
ipv6.google.com.        32      IN      CNAME   ipv6.l.google.com.
ipv6.l.google.com.      21      IN      AAAA    2607:f8b0:400b:807::200e

;; Query time: 3 msec
;; SERVER: 10.255.255.254#53(10.255.255.254) (UDP)
;; WHEN: Sun Oct 19 15:18:13 EDT 2025
;; MSG SIZE  rcvd: 103
```
