# DNS

<https://www.cloudflare.com/learning/dns/dns-records/>

<https://zytrax.com/books/dns/>

<https://www.cloudflare.com/learning/dns/what-is-1.1.1.1/>

## nslookup

<https://www.linode.com/docs/guides/how-to-use-nslookup-command/>

```console
ubuntu@LAPTOP-JBell:~$ nslookup wikipedia.org
Server:         10.255.255.254
Address:        10.255.255.254#53

Non-authoritative answer:
Name:   wikipedia.org
Address: 208.80.154.224
Name:   wikipedia.org
Address: 2620:0:861:ed1a::1
```

```console
ubuntu@LAPTOP-JBell:~$ nslookup wikipedia.org 9.9.9.9
Server:         9.9.9.9
Address:        9.9.9.9#53

Non-authoritative answer:
Name:   wikipedia.org
Address: 208.80.154.224
Name:   wikipedia.org
Address: 2620:0:861:ed1a::1
```

### `-type=ns`

```console
ubuntu@LAPTOP-JBell:~$ nslookup -type=ns wikipedia.org
Server:         10.255.255.254
Address:        10.255.255.254#53

Non-authoritative answer:
wikipedia.org   nameserver = ns0.wikimedia.org.
wikipedia.org   nameserver = ns1.wikimedia.org.
wikipedia.org   nameserver = ns2.wikimedia.org.

Authoritative answers can be found from:

```

```console
ubuntu@LAPTOP-JBell:~$ nslookup wikipedia.org ns0.wikimedia.org
Server:         ns0.wikimedia.org
Address:        208.80.154.238#53

Name:   wikipedia.org
Address: 208.80.154.224
Name:   wikipedia.org
Address: 2620:0:861:ed1a::1
```

### `-type=mx`

```console
ubuntu@LAPTOP-JBell:~$ nslookup -type=mx wikipedia.org
Server:         10.255.255.254
Address:        10.255.255.254#53

Non-authoritative answer:
wikipedia.org   mail exchanger = 10 mx-in1001.wikimedia.org.
wikipedia.org   mail exchanger = 10 mx-in2001.wikimedia.org.

Authoritative answers can be found from:

```

### `-type=soa`

```console
ubuntu@LAPTOP-JBell:~$ nslookup -type=soa wikipedia.org
Server:         10.255.255.254
Address:        10.255.255.254#53

Non-authoritative answer:
wikipedia.org
        origin = ns0.wikimedia.org
        mail addr = hostmaster.wikimedia.org
        serial = 2025101418
        refresh = 43200
        retry = 7200
        expire = 1209600
        minimum = 3600

Authoritative answers can be found from:

```

### `-type=txt`

```console
ubuntu@LAPTOP-JBell:~$ nslookup -type=txt wikipedia.org
Server:         10.255.255.254
Address:        10.255.255.254#53

Non-authoritative answer:
wikipedia.org   text = "yandex-verification: 35c08d23099dc863"
wikipedia.org   text = "v=spf1 include:_cidrs.wikimedia.org ~all"
wikipedia.org   text = "google-site-verification=AMHkgs-4ViEvIJf5znZle-BSE2EPNFqM1nDJGRyn2qk"

Authoritative answers can be found from:

```

## dig

<https://www.linode.com/docs/guides/use-dig-to-perform-manual-dns-queries/>

```console
ubuntu@LAPTOP-JBell:~$ dig wikipedia.org

; <<>> DiG 9.18.30-0ubuntu0.22.04.2-Ubuntu <<>> wikipedia.org
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 12075
;; flags: qr rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 1232
;; QUESTION SECTION:
;wikipedia.org.                 IN      A

;; ANSWER SECTION:
wikipedia.org.          43      IN      A       208.80.154.224

;; Query time: 24 msec
;; SERVER: 10.255.255.254#53(10.255.255.254) (UDP)
;; WHEN: Sat Oct 18 14:50:42 EDT 2025
;; MSG SIZE  rcvd: 58

```

### dig @

```console
ubuntu@LAPTOP-JBell:~$ dig @1.1.1.1 google.com

; <<>> DiG 9.18.30-0ubuntu0.22.04.2-Ubuntu <<>> @1.1.1.1 google.com
; (1 server found)
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 17621
;; flags: qr rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 1232
;; QUESTION SECTION:
;google.com.                    IN      A

;; ANSWER SECTION:
google.com.             292     IN      A       142.251.33.174

;; Query time: 4 msec
;; SERVER: 1.1.1.1#53(1.1.1.1) (UDP)
;; WHEN: Sat Oct 18 14:59:37 EDT 2025
;; MSG SIZE  rcvd: 55

```

## host

<https://linux.die.net/man/1/host>

```console
ubuntu@LAPTOP-JBell:~$ host google.com
google.com has address 142.251.41.78
google.com has IPv6 address 2607:f8b0:400b:80c::200e
google.com mail is handled by 10 smtp.google.com.
```

```console
ubuntu@LAPTOP-JBell:~$ host -C google.com
;; UDP setup with 2001:4860:4802:36::a#53(2001:4860:4802:36::a) for google.com failed: network unreachable.
;; UDP setup with 2001:4860:4802:34::a#53(2001:4860:4802:34::a) for google.com failed: network unreachable.
;; UDP setup with 2001:4860:4802:32::a#53(2001:4860:4802:32::a) for google.com failed: network unreachable.
;; UDP setup with 2001:4860:4802:38::a#53(2001:4860:4802:38::a) for google.com failed: network unreachable.
Nameserver 216.239.34.10:
        google.com has SOA record ns1.google.com. dns-admin.google.com. 820613609 900 900 1800 60
Nameserver 216.239.38.10:
        google.com has SOA record ns1.google.com. dns-admin.google.com. 820613609 900 900 1800 60
Nameserver 216.239.32.10:
        google.com has SOA record ns1.google.com. dns-admin.google.com. 820613609 900 900 1800 60
Nameserver 216.239.36.10:
        google.com has SOA record ns1.google.com. dns-admin.google.com. 820613609 900 900 1800 60
```

```console
ubuntu@LAPTOP-JBell:~$ host -t MX google.com
google.com mail is handled by 10 smtp.google.com.
```

```console
ubuntu@LAPTOP-JBell:~$ host -t SOA google.com
google.com has SOA record ns1.google.com. dns-admin.google.com. 820613609 900 900 1800 60
```

```console
ubuntu@LAPTOP-JBell:~$ host -t TXT google.com
google.com descriptive text "facebook-domain-verification=22rm551cu4k0ab0bxsw536tlds4h95"
google.com descriptive text "google-site-verification=wD8N7i1JTNTkezJ49swvWW48f8_9xveREV4oB-0Hf5o"
google.com descriptive text "docusign=05958488-4752-4ef2-95eb-aa7ba8a3bd0e"
google.com descriptive text "globalsign-smime-dv=CDYX+XFHUw2wml6/Gb8+59BsH31KzUr6c1l2BPvqKX8="
google.com descriptive text "cisco-ci-domain-verification=47c38bc8c4b74b7233e9053220c1bbe76bcc1cd33c7acf7acd36cd6a5332004b"
google.com descriptive text "google-site-verification=TV9-DBe4R80X4v0M4U_bd_J9cpOJM0nikft0jAgjmsQ"
google.com descriptive text "v=spf1 include:_spf.google.com ~all"
google.com descriptive text "apple-domain-verification=30afIBcvSuDV2PLX"
google.com descriptive text "docusign=1b0a6754-49b1-4db5-8540-d2c12664b289"
google.com descriptive text "google-site-verification=4ibFUgB-wXLQ_S7vsXVomSTVamuOXBiVAzpR5IZ87D0"
google.com descriptive text "onetrust-domain-verification=de01ed21f2fa4d8781cbc3ffb89cf4ef"
google.com descriptive text "MS=E4A68B9AB2BB9670BCE15412F62916164C0B20BB"
```

## getent

<https://linux.die.net/man/1/getent>

```console
ubuntu@LAPTOP-JBell:~$ getent ahosts wikipedia.org
208.80.154.224  STREAM wikipedia.org
208.80.154.224  DGRAM
208.80.154.224  RAW
2620:0:861:ed1a::1 STREAM
2620:0:861:ed1a::1 DGRAM
2620:0:861:ed1a::1 RAW
```

## whois (WHOIS Protocol, RFC 3912)

<https://www.iana.org/whois>

<https://www.arin.net/resources/registry/whois/rws/cli/>

```console
ubuntu@LAPTOP-JBell:~$ whois google.com
   Domain Name: GOOGLE.COM
   Registry Domain ID: 2138514_DOMAIN_COM-VRSN
   Registrar WHOIS Server: whois.markmonitor.com
   Registrar URL: http://www.markmonitor.com
   Updated Date: 2019-09-09T15:39:04Z
   Creation Date: 1997-09-15T04:00:00Z
   Registry Expiry Date: 2028-09-14T04:00:00Z
   Registrar: MarkMonitor Inc.
   Registrar IANA ID: 292
   Registrar Abuse Contact Email: abusecomplaints@markmonitor.com
   Registrar Abuse Contact Phone: +1.2086851750
   Domain Status: clientDeleteProhibited https://icann.org/epp#clientDeleteProhibited
   Domain Status: clientTransferProhibited https://icann.org/epp#clientTransferProhibited
   Domain Status: clientUpdateProhibited https://icann.org/epp#clientUpdateProhibited
   Domain Status: serverDeleteProhibited https://icann.org/epp#serverDeleteProhibited
   Domain Status: serverTransferProhibited https://icann.org/epp#serverTransferProhibited
   Domain Status: serverUpdateProhibited https://icann.org/epp#serverUpdateProhibited
   Name Server: NS1.GOOGLE.COM
   Name Server: NS2.GOOGLE.COM
   Name Server: NS3.GOOGLE.COM
   Name Server: NS4.GOOGLE.COM
   DNSSEC: unsigned
   URL of the ICANN Whois Inaccuracy Complaint Form: https://www.icann.org/wicf/
>>> Last update of whois database: 2025-10-18T19:06:54Z <<<
```

## rdap

<https://www.icann.org/en/contracted-parties/registry-operators/resources/registration-data-access-protocol>

> The Registration Data Access Protocol (RDAP) enables users to access current registration data and was created as an eventual replacement for the WHOIS protocol. RDAP was developed by the technical community in the Internet Engineering Task Force (IETF).
>
> RDAP is a protocol that delivers registration data like WHOIS, but its implementation will change and standardize data access and query response formats. RDAP has several advantages over the WHOIS protocol, including support for internationalization, secure access to data, and the ability to provide differentiated access to registration data.

<https://www.openrdap.org/>
