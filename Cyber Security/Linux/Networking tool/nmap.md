`-p 80` scan port 80
`-p 1000-1500` scan ports from 1000 to 1500
`-p-` scan all ports

`-A` aggressive mode

`-sS` Syn scan 
`-sU` UDP scan
`-O` detect OS
`-sV` detect the version of services running

`-v` verbose
`-vv` more verbose

saving outputs:
`-oA` save to 3 major format at once
`-oN` normal format
`-oG` grepable format

timing:
`-T5` timing template to level 5

scripts:
`--script=vuln` activate all scripts in "vuln" category

TCP scan:
`-ST` connect scans
`-sS` SYN "half-open" scans
`-sN` TCP full scan
`-sF` TCP FIN scans
`-sX` TCP Xmas Scans

## TCP connection scan
if port is closed, response RST instead of SYN/ACK:
![](https://i.imgur.com/xzUSnqT.png)


firewall reject TCP SYN with RST instead of drop it
`iptables -I INPUT -p tcp --dport <port> -j REJECT --reject-with tcp-reset`

## SYN scan
also referred to as "half-open" / "stealth" scans

![](https://i.imgur.com/vGvC9by.png)

send RST after SYN/ACK

PROs:
* by bass some old Intrusion-detection system
* not logged by application
* significantly faster

CONs:
* need sudo permission
* sometimes brought down unstable services

SYN scan is default if you running in SUDO
otherwise, TCP scan is default.