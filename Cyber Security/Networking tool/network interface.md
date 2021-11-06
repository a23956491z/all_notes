/etc/udev/rules.d/10-network.rules
```
SUBSYSTEM=="net", ACTION=="add", ATTR{address}=="d8:5e:d3:05:93:16", NAME="eno1"
```

static ip:
disable `systemd-networkd` first

```bash
systemctl disable systemd-networkd
systemctl stop systemd-networkd
```

```bash
systemctl enable dhcpcd
systemctl start dhcpcd
```

edit `/etc/dhcpcd.conf`
```
interface eno1
static ip_address=134.208.3.188/24
static routers=134.208.3.254
static domain_name_servers=8.8.8.8 8.8.4.4 1.1.1.1
```