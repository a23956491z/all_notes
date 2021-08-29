Server:
```bash
sudo pacman -S openssh
sudo sshd -t
```

**SSH 的IP ADDR如果設固定IP，可能會無法在開機時啓動**
> 之前設 134.208.3.198時 會掛掉，設0.0.0.0可能比較好


`/etc/ssh/sshd_config`
```
PermitRootLogin no
Port 22
PasswordAuthentication no
HostKey /etc/ssh/ssh_host_rsa_key
```


```bash
ssh-keygen -t dsa -f /etc/ssh/ssh_host_dsa_key
ssh-keygen -t rsa -f /etc/ssh/ssh_host_rsa_key
# keyphase empty
    
chmod 600 /etc/ssh/ssh_host_dsa_key
chmod 600 /etc/ssh/ssh_host_rsa_key
```


Client:
~/.ssh/config
```
# host-specific options
Host arch
    User enip
    Hostname 192.168.56.101
    Port     33874
```

bad owner or permission
```bash
chmod 600 ~/.ssh/config
# change from 644 to 600
chown $USER ~/.ssh/config
# change user
```

copy key to server
```bash
$ ssh-copy-id -p 33874 enip@192.168.56.101
```