# dmidecode

> dmidecode is a tool for dumping a computer's DMI (some say SMBIOS ) table contents in a human-readable format. This table contains a description of the system's hardware components,
> as well as other useful pieces of information such as serial numbers and BIOS revision. Thanks to this table, you can retrieve this information without having to probe for the actual
> hardware. While this is a good point in terms of report speed and safeness, this also makes the presented information possibly unreliable.

<https://linux.die.net/man/8/dmidecode>

<https://savannah.nongnu.org/projects/dmidecode/>

## SMBIOS

<https://www.dmtf.org/standards/smbios>

> SMBIOS is the premier standard for delivering management information via system firmware. Since its release in 1995, the widely implemented SMBIOS standard has
> simplified the management of more than two billion client and server systems.
>
> For OS-present, OS-absent, and pre-OS environments, SMBIOS offers motherboard and system vendors a standard format to present management information about their products.
> By extending the system firmware interface, SMBIOS can be used with management applications that use DMTF’s Common Information Model (CIM)  or another technology, such as SNMP.
> It eliminates the need for error-prone operations, such as probing system hardware for presence detection.
>
> Originally designed for Intel® processor architecture systems, SMBIOS now includes support for IA-32 (x86), x64 (x86-64, Intel64, AMD64, EM64T), Intel® Itanium® architecture,
> 32-bit ARM (Aarch32) and 64-bit ARM (Aarch64).

## WSL 2

```console
ubuntu@LAPTOP-JBell:~$ sudo dmidecode --type 17
[sudo] password for ubuntu:
# dmidecode 3.3
Scanning /dev/mem for entry point.
# No SMBIOS nor DMI entry point found, sorry.
```

## Hyper-V Manager

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
