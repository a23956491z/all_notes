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