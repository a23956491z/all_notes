```bash
sudo pacman -S tigervnc
```

create password
`vncpasswd`

開放 VNC 的帳號盡可能不要有太多權限
edit `/etc/tigervnc/vncserver.users`
```
:1=kambel
```

建議加上 `localhost`
避免直接 expose VNC port 增加風險
可以 SSH 到 server 後，藉由 Tunnel 使用 VNC

create `~/.vnc/config`
```
session=xfce
geometry=1920x1080
localhost
alwaysshared
```





## Connect with ssh
在 localhost 架一個 tunnel 到 server的 5901 port
然後這個 Tunnel 的資訊都會經過 SSH
```bash
$ ssh 10.1.10.2 -L 9901:localhost:5901
```

```bash
$ vncviewer localhost:9901
```