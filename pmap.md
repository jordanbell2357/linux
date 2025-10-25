# pmap

<https://man7.org/linux/man-pages/man1/pmap.1.html>

```console
ubuntu@LAPTOP-JBell:~$ head -c 1G /dev/zero | pv -q -L 100M | tail > /dev/null & (sleep 5; pmap $(pidof tail | cut -d ' ' -f 1))
[4] 13411
13411:   tail
00005e14916d9000      8K r---- tail
00005e14916db000     40K r-x-- tail
00005e14916e5000     12K r---- tail
00005e14916e9000      4K r---- tail
00005e14916ea000      4K rw--- tail
00005e14ba927000 514448K rw---   [ anon ]
0000799dd6600000    160K r---- libc.so.6
0000799dd6628000   1620K r-x-- libc.so.6
0000799dd67bd000    352K r---- libc.so.6
0000799dd6815000      4K ----- libc.so.6
0000799dd6816000     16K r---- libc.so.6
0000799dd681a000      8K rw--- libc.so.6
0000799dd681c000     52K rw---   [ anon ]
0000799dd69a9000    348K r---- LC_CTYPE
0000799dd6a00000      4K r---- LC_NUMERIC
0000799dd6a01000      4K r---- LC_TIME
0000799dd6a02000      4K r---- LC_COLLATE
0000799dd6a03000     12K rw---   [ anon ]
0000799dd6a06000      4K r---- LC_MONETARY
0000799dd6a07000      4K r---- SYS_LC_MESSAGES
0000799dd6a08000      4K r---- LC_PAPER
0000799dd6a09000      4K r---- LC_NAME
0000799dd6a0a000      4K r---- LC_ADDRESS
0000799dd6a0b000      4K r---- LC_TELEPHONE
0000799dd6a0c000      4K r---- LC_MEASUREMENT
0000799dd6a0d000     28K r--s- gconv-modules.cache
0000799dd6a14000      8K rw---   [ anon ]
0000799dd6a16000      8K r---- ld-linux-x86-64.so.2
0000799dd6a18000    168K r-x-- ld-linux-x86-64.so.2
0000799dd6a42000     44K r---- ld-linux-x86-64.so.2
0000799dd6a4d000      4K r---- LC_IDENTIFICATION
0000799dd6a4e000      8K r---- ld-linux-x86-64.so.2
0000799dd6a50000      8K rw--- ld-linux-x86-64.so.2
00007ffe72317000    136K rw---   [ stack ]
00007ffe72384000     16K r----   [ anon ]
00007ffe72388000      8K r-x--   [ anon ]
 total           517564K
```


```console
ubuntu@LAPTOP-JBell:~$ head -c 1G /dev/zero | pv -q -L 100M | tail > /dev/null & (sleep 7; pmap $(pidof tail | cut -d '
' -f 1))
[4] 13423
13423:   tail
000064bbf35c6000      8K r---- tail
000064bbf35c8000     40K r-x-- tail
000064bbf35d2000     12K r---- tail
000064bbf35d6000      4K r---- tail
000064bbf35d7000      4K rw--- tail
000064bc1a2cd000 720088K rw---   [ anon ]
000075bdd3a00000    160K r---- libc.so.6
000075bdd3a28000   1620K r-x-- libc.so.6
000075bdd3bbd000    352K r---- libc.so.6
000075bdd3c15000      4K ----- libc.so.6
000075bdd3c16000     16K r---- libc.so.6
000075bdd3c1a000      8K rw--- libc.so.6
000075bdd3c1c000     52K rw---   [ anon ]
000075bdd3d85000    348K r---- LC_CTYPE
000075bdd3ddc000      4K r---- LC_NUMERIC
000075bdd3ddd000      4K r---- LC_TIME
000075bdd3dde000      4K r---- LC_COLLATE
000075bdd3ddf000     12K rw---   [ anon ]
000075bdd3de2000      4K r---- LC_MONETARY
000075bdd3de3000      4K r---- SYS_LC_MESSAGES
000075bdd3de4000      4K r---- LC_PAPER
000075bdd3de5000      4K r---- LC_NAME
000075bdd3de6000      4K r---- LC_ADDRESS
000075bdd3de7000      4K r---- LC_TELEPHONE
000075bdd3de8000      4K r---- LC_MEASUREMENT
000075bdd3de9000     28K r--s- gconv-modules.cache
000075bdd3df0000      8K rw---   [ anon ]
000075bdd3df2000      8K r---- ld-linux-x86-64.so.2
000075bdd3df4000    168K r-x-- ld-linux-x86-64.so.2
000075bdd3e1e000     44K r---- ld-linux-x86-64.so.2
000075bdd3e29000      4K r---- LC_IDENTIFICATION
000075bdd3e2a000      8K r---- ld-linux-x86-64.so.2
000075bdd3e2c000      8K rw--- ld-linux-x86-64.so.2
00007ffd24cb7000    136K rw---   [ stack ]
00007ffd24d9a000     16K r----   [ anon ]
00007ffd24d9e000      8K r-x--   [ anon ]
 total           723204K
```
