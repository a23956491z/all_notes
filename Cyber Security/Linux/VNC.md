```bash
sudo pacman -S tigervnc
```

create password
`vncpasswd`

edit `/etc/tigervnc/vncserver.users`
```
:1=enip
```

create `~/.vnc/config`
```
session=xfce
geometry=1920x1080
localhost
alwaysshared
```

