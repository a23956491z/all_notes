check DHCP devices
```bash
cat /tmp/dhcp.leases
```

check internet inferface
```bash
ifconfig
```

## Setting in SWITCH
802.1Q VLAN
* VLAN ID : 10, VLAN NAME : WAN
	* not member : port 3~8
	* tag (trunk) : port 1, 2
* VLAN ID : 1, VLAN NAME : LAN
	* not member : port 1
	* Untagged : port 2~8

802.1Q PVID setting
* port 1 : PVID 10

```bash
$ vi /etc/config/network
```
 
```bash
config interface 'wan'
	option ifname 'eth0.10'
	option proto 'static'
	option ipaddr '134.208.3.198'
	option netmask '255.255.255.0'
	option gateway '134.208.3.254'
	option dns  '8.8.8.8'
```

## Configure WIFI
MSI laptop example: Intel AC9560
Intel Wireless 8260


```bash
$ lspci
```

```bash
$ opkg update
$ opkg install pciutils
```

install firmware & driver on OpenWRT
```bash
$ opkg install ath10k-firware...
$ opkg install ath10k-ct
```

Enable WPA wifi security:
* install `hostapd`

## Benchmark
from inside wireless router to wired:
 134.208.3.184 (inside router) -> 134.208.3.186
 `58.9 Mbits/s`

wired to wired from switch:
134.208.3.198 -> 134.208.3.186

by wireless to wireless inside router LAN:
from 192.168.0.147 -> 192.168.0.150
`60.5 Mbits/s`

