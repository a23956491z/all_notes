/etc/udev/rules.d/10-network.rules
```
SUBSYSTEM=="net", ACTION=="add", ATTR{address}=="d8:5e:d3:05:93:16", NAME="eno1"
```