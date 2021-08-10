```bash
cat /tmp/dhcp.leases
```

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