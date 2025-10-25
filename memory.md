# Memory monitoring in Linux

## /proc/meminfo

```console
ubuntu@LAPTOP-JBell:~$ cat /proc/meminfo
MemTotal:        7989432 kB
MemFree:         4235404 kB
MemAvailable:    4877840 kB
Buffers:           16000 kB
Cached:           596828 kB
SwapCached:           32 kB
Active:           445392 kB
Inactive:        2519392 kB
Active(anon):       9504 kB
Inactive(anon):  2367640 kB
Active(file):     435888 kB
Inactive(file):   151752 kB
Unevictable:           0 kB
Mlocked:               0 kB
SwapTotal:       2097152 kB
SwapFree:        2095860 kB
Dirty:                 4 kB
Writeback:             0 kB
AnonPages:       2352300 kB
Mapped:           602496 kB
Shmem:             25168 kB
KReclaimable:     251008 kB
Slab:             389600 kB
SReclaimable:     251008 kB
SUnreclaim:       138592 kB
KernelStack:       17376 kB
PageTables:        49248 kB
SecPageTables:         0 kB
NFS_Unstable:          0 kB
Bounce:                0 kB
WritebackTmp:          0 kB
CommitLimit:     6091868 kB
Committed_AS:    5555920 kB
VmallocTotal:   34359738367 kB
VmallocUsed:       48160 kB
VmallocChunk:          0 kB
Percpu:             9536 kB
HardwareCorrupted:     0 kB
AnonHugePages:         0 kB
ShmemHugePages:        0 kB
ShmemPmdMapped:        0 kB
FileHugePages:         0 kB
FilePmdMapped:         0 kB
Unaccepted:            0 kB
HugePages_Total:       0
HugePages_Free:        0
HugePages_Rsvd:        0
HugePages_Surp:        0
Hugepagesize:       2048 kB
Hugetlb:               0 kB
DirectMap4k:      236544 kB
DirectMap2M:     8007680 kB
DirectMap1G:     8388608 kB
ubuntu@LAPTOP-JBell:~$ cat /proc/meminfo | grep MemTotal
MemTotal:        7989432 kB
ubuntu@LAPTOP-JBell:~$ cat /proc/meminfo | grep MemFree
MemFree:         4237356 kB
ubuntu@LAPTOP-JBell:~$ cat /proc/meminfo | grep MemAvailable
MemAvailable:    4879612 kB
ubuntu@LAPTOP-JBell:~$ cat /proc/meminfo | grep MemTotal | tr -s ' ' '\t'
MemTotal:       7989432 kB
ubuntu@LAPTOP-JBell:~$ cat /proc/meminfo | grep MemTotal | tr -s ' ' '\t' | cut -f 2
7989432
```

## free

<https://www.linuxfoundation.org/blog/blog/classic-sysadmin-linux-101-5-commands-for-checking-memory-usage-in-linux>

```console
ubuntu@LAPTOP-JBell:~$ free -m | sed -n '2p' | tr -s ' ' '\t'
Mem:    7802    2875    4088    24      838     4710
ubuntu@LAPTOP-JBell:~$ free -m
               total        used        free      shared  buff/cache   available
Mem:            7802        2873        4089          24         838        4712
Swap:           2048           1        2046
ubuntu@LAPTOP-JBell:~$ free -m | sed -n '2p'
Mem:            7802        2875        4088          24         838        4710
ubuntu@LAPTOP-JBell:~$ free -m | sed -n '2p' | tr -s ' ' '\t'
Mem:    7802    2873    4089    24      838     4712
ubuntu@LAPTOP-JBell:~$ free -m | sed -n '2p' | tr -s '[:space:]' '\t' | cut -f 2
7802
ubuntu@LAPTOP-JBell:~$ free -m | sed -n '2p' | tr -s '[:space:]' '\t' | cut -f 4
4089
```

## vmstat

```console
ubuntu@LAPTOP-JBell:~$ vmstat --unit M -s
         7802 M total memory
         2812 M used memory
          431 M active memory
         2455 M inactive memory
         4149 M free memory
           14 M buffer memory
          825 M swap cache
         2048 M total swap
            1 M used swap
         2046 M free swap
       479520 non-nice user cpu ticks
           72 nice user cpu ticks
       662132 system cpu ticks
    374904227 idle cpu ticks
        62102 IO-wait cpu ticks
            0 IRQ cpu ticks
        98846 softirq cpu ticks
            0 stolen cpu ticks
     10449089 pages paged in
     38058836 pages paged out
            6 pages swapped in
           92 pages swapped out
    206632904 interrupts
    306925062 CPU context switches
   1760141965 boot time
       859314 forks
ubuntu@LAPTOP-JBell:~$ vmstat --unit M -s | grep "total memory"
         7802 M total memory
ubuntu@LAPTOP-JBell:~$ vmstat --unit M -s | grep "total memory" | sed -r 's/^[[:space:]]*([[:digit:]]+).*/\1/'
7802
ubuntu@LAPTOP-JBell:~$ vmstat --unit M -s | grep "free memory" | sed -r 's/^[[:space:]]*([[:digit:]]+).*/\1/'
4136
```

## lsmem

<https://man7.org/linux/man-pages/man1/lsmem.1.html>

```console
ubuntu@LAPTOP-JBell:~$ lsmem
RANGE                                  SIZE  STATE REMOVABLE BLOCK
0x0000000000000000-0x00000000f7ffffff  3.9G online       yes  0-30
0x0000000100000000-0x00000001ffffffff    4G online       yes 32-63

Memory block size:       128M
Total online memory:     7.9G
Total offline memory:      0B
```

## dmidecode

> dmidecode is a tool for dumping a computer's DMI (some say SMBIOS ) table contents in a human-readable format. This table contains a description of the system's hardware components, as well as other useful pieces of information such as serial numbers and BIOS revision. Thanks to this table, you can retrieve this information without having to probe for the actual hardware. While this is a good point in terms of report speed and safeness, this also makes the presented information possibly unreliable.

<https://linux.die.net/man/8/dmidecode>

<https://www.dmtf.org/standards/smbios>

<https://savannah.nongnu.org/projects/dmidecode/>

### WSL 2

```console
ubuntu@LAPTOP-JBell:~$ sudo dmidecode --type 17
[sudo] password for ubuntu:
# dmidecode 3.3
Scanning /dev/mem for entry point.
# No SMBIOS nor DMI entry point found, sorry.
```

### Hyper-V Manager

<https://learn.microsoft.com/en-us/windows-server/virtualization/hyper-v/get-started/install-hyper-v?tabs=powershell&pivots=windows>

<https://learn.microsoft.com/en-us/training/paths/windows-server-hyper-v-virtualization/>

```console
ubuntu@ubuntu-vm:~/Desktop$ sudo dmidecode -t 17
[sudo] password for ubuntu: 
# dmidecode 3.3
Getting SMBIOS data from sysfs.
SMBIOS 3.1.0 present.

Handle 0x0006, DMI type 16, 23 bytes
Physical Memory Array
	Location: System Board Or Motherboard
	Use: System Memory
	Error Correction Type: None
	Maximum Capacity: 0 bytes
	Error Information Handle: Not Provided
	Number Of Devices: 2

Handle 0x0007, DMI type 17, 92 bytes
Memory Device
	Array Handle: 0x0006
	Error Information Handle: Not Provided
	Total Width: Unknown
	Data Width: Unknown
	Size: 3968 MB
	Form Factor: Unknown
	Set: None
	Locator: M0001
	Bank Locator: None
	Type: Unknown
	Type Detail: Unknown
	Speed: Unknown
	Manufacturer: Microsoft Corporation
	Serial Number: None
	Asset Tag: None
	Part Number: None
	Rank: Unknown
	Configured Memory Speed: Unknown
	Minimum Voltage: Unknown
	Maximum Voltage: Unknown
	Configured Voltage: Unknown
	Memory Technology: <OUT OF SPEC>
	Memory Operating Mode Capability: None
	Firmware Version: Not Specified
	Module Manufacturer ID: Unknown
	Module Product ID: Unknown
	Memory Subsystem Controller Manufacturer ID: Unknown
	Memory Subsystem Controller Product ID: Unknown
	Non-Volatile Size: None
	Volatile Size: None
	Cache Size: None
	Logical Size: None

Handle 0x000A, DMI type 17, 92 bytes
Memory Device
	Array Handle: 0x0006
	Error Information Handle: Not Provided
	Total Width: Unknown
	Data Width: Unknown
	Size: 128 MB
	Form Factor: Unknown
	Set: None
	Locator: M0002
	Bank Locator: None
	Type: Unknown
	Type Detail: Unknown
	Speed: Unknown
	Manufacturer: Microsoft Corporation
	Serial Number: None
	Asset Tag: None
	Part Number: None
	Rank: Unknown
	Configured Memory Speed: Unknown
	Minimum Voltage: Unknown
	Maximum Voltage: Unknown
	Configured Voltage: Unknown
	Memory Technology: <OUT OF SPEC>
	Memory Operating Mode Capability: None
	Firmware Version: Not Specified
	Module Manufacturer ID: Unknown
	Module Product ID: Unknown
	Memory Subsystem Controller Manufacturer ID: Unknown
	Memory Subsystem Controller Product ID: Unknown
	Non-Volatile Size: None
	Volatile Size: None
	Cache Size: None
	Logical Size: None

```
