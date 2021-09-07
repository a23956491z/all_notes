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

## UDP scan
`-sU`

packet is sent to an open UDP port, should be **no response**
and when it comes with no response, it could be `open|filtered`.
* port is open
* or be firewalled

packet is sent to an closed port, target whould respnd with an ICMP packet containing message that the port is unreachable.

and UDP scans tend to be so slow, so usually run with `--top-ports <number>`
```bash
nmap -sU --top-ports 20 <target>
```

## NULL / FIN / Xmas scan
more stealthier

used for  firewall evasion

some firewall drop incoming TCP packets to blocked ports which have SYN flag set

## ICMP scan
ping sweep `-sn`

```bash
nmap -sn 192.168.0.1-254
nmap -sn 192.168.0.*
nmap -sn 192.168.0.0/24
```

## NSE scripts
categories:
* safe
* intrusive : may affect the target
* vuln
* exploit : exploit a vulerability
* auth :  bypass authentication 
* brute : bruteforce credentials  
* discovery

running with scripts `--script=<script-name>`
multiple scripts `--script=smb-enum-users,smb-enum-shares`

arguments
`nmap -p 80 --script http-put --script-args http-put.url='/dav/shell.php',http-put.file='./shell.php'`

script help: `nmap --script-help <script-name>`

