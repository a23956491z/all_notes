```bash
sudo pacman -S openssh
```

PermitRootLogin no
Port 22
PasswordAuthentication no
HostKey /etc/ssh/ssh_host_rsa_key

```bash
ssh-keygen -t dsa -f /etc/ssh/ssh_host_dsa_key
ssh-keygen -t rsa -f /etc/ssh/ssh_host_rsa_key
# keyphase empty
    
chmod 600 /etc/ssh/ssh_host_dsa_key
chmod 600 /etc/ssh/ssh_host_rsa_key
```