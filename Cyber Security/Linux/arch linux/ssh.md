```bash
sudo pacman -S openssh
```

PermitRootLogin no
Port 22
PasswordAuthentication no

```bash
sh-keygen -t dsa -f /etc/ssh/ssh_host_dsa_key
ssh-keygen -t rsa -f /etc/ssh/ssh_host_rsa_key

    
chmod 600 /etc/ssh/ssh_host_dsa_key
chmod 600 /etc/ssh/ssh_host_rsa_key
```