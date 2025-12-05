# ssh -R

<https://pinggy.io/amp/blog/ssh_reverse_tunnelling/>

```bash
sudo vi /etc/ssh/sshd_config
```

```
#GatewayPorts no
```

to

```
GatewayPorts yes
```

Then

```bash
sudo systemctl restart sshd
```

On local machine,

```bash
ssh -R 3001:localhost:3002 ubuntu@histfile.org
```

This logs us into the remote machine. While this session is active, we run tcpdump and then curl

```bash
sudo tcpdump -w port3002.pcap port 3002
```

Then

```bash
timeout -s SIGTERM 1 curl histfile.org:3001
```

and we check what tcpdump has captured:

```
20 packets received by filter
0 packets dropped by kernel
```

```bash
tshark -r port3002.pcap
```

```
    1   0.000000    127.0.0.1 → 127.0.0.1    TCP 74 46078 → 3002 [SYN] Seq=0 Win=64240 Len=0 MSS=1460 SACK_PERM TSval=2816806178 TSecr=0 WS=128
    2   0.000231    127.0.0.1 → 127.0.0.1    TCP 54 3002 → 64731 [RST, ACK] Seq=1 Ack=1 Win=0 Len=0
    3   1.021672    127.0.0.1 → 127.0.0.1    TCP 74 [TCP Retransmission] 46078 → 3002 [SYN] Seq=0 Win=64240 Len=0 MSS=1460 SACK_PERM TSval=2816807200 TSecr=0 WS=128
    4   1.022351    127.0.0.1 → 127.0.0.1    TCP 54 3002 → 64731 [RST, ACK] Seq=1 Ack=1 Win=0 Len=0
    5   1.309732    127.0.0.1 → 127.0.0.1    TCP 74 47850 → 3002 [SYN] Seq=0 Win=64240 Len=0 MSS=1460 SACK_PERM TSval=2816807488 TSecr=0 WS=128
    6   1.310145    127.0.0.1 → 127.0.0.1    TCP 54 3002 → 31286 [RST, ACK] Seq=1 Ack=1 Win=0 Len=0
    7   2.045712    127.0.0.1 → 127.0.0.1    TCP 74 [TCP Retransmission] 46078 → 3002 [SYN] Seq=0 Win=64240 Len=0 MSS=1460 SACK_PERM TSval=2816808224 TSecr=0 WS=128
    8   2.046495    127.0.0.1 → 127.0.0.1    TCP 54 3002 → 64731 [RST, ACK] Seq=1 Ack=1 Win=0 Len=0
    9   3.069715    127.0.0.1 → 127.0.0.1    TCP 74 [TCP Retransmission] 46078 → 3002 [SYN] Seq=0 Win=64240 Len=0 MSS=1460 SACK_PERM TSval=2816809248 TSecr=0 WS=128
   10   3.070449    127.0.0.1 → 127.0.0.1    TCP 54 3002 → 64731 [RST, ACK] Seq=1 Ack=1 Win=0 Len=0
   11   4.093711    127.0.0.1 → 127.0.0.1    TCP 74 [TCP Retransmission] 46078 → 3002 [SYN] Seq=0 Win=64240 Len=0 MSS=1460 SACK_PERM TSval=2816810272 TSecr=0 WS=128
   12   4.094424    127.0.0.1 → 127.0.0.1    TCP 54 3002 → 64731 [RST, ACK] Seq=1 Ack=1 Win=0 Len=0
   13   5.117777    127.0.0.1 → 127.0.0.1    TCP 74 [TCP Retransmission] 46078 → 3002 [SYN] Seq=0 Win=64240 Len=0 MSS=1460 SACK_PERM TSval=2816811296 TSecr=0 WS=128
   14   5.118485    127.0.0.1 → 127.0.0.1    TCP 54 3002 → 64731 [RST, ACK] Seq=1 Ack=1 Win=0 Len=0
   15   7.133668    127.0.0.1 → 127.0.0.1    TCP 74 [TCP Retransmission] 46078 → 3002 [SYN] Seq=0 Win=64240 Len=0 MSS=1460 SACK_PERM TSval=2816813312 TSecr=0 WS=128
   16   7.134467    127.0.0.1 → 127.0.0.1    TCP 54 3002 → 64731 [RST, ACK] Seq=1 Ack=1 Win=0 Len=0
   17  11.293574    127.0.0.1 → 127.0.0.1    TCP 74 [TCP Retransmission] 46078 → 3002 [SYN] Seq=0 Win=64240 Len=0 MSS=1460 SACK_PERM TSval=2816817472 TSecr=0 WS=128
   18  11.293999    127.0.0.1 → 127.0.0.1    TCP 54 3002 → 64731 [RST, ACK] Seq=1 Ack=1 Win=0 Len=0
   19  19.485514    127.0.0.1 → 127.0.0.1    TCP 74 [TCP Retransmission] 46078 → 3002 [SYN] Seq=0 Win=64240 Len=0 MSS=1460 SACK_PERM TSval=2816825664 TSecr=0 WS=128
   20  19.485796    127.0.0.1 → 127.0.0.1    TCP 54 3002 → 64731 [RST, ACK] Seq=1 Ack=1 Win=0 Len=0
```

