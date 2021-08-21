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



## Connect with ssh
```bash
$ ssh 10.1.10.2 -L 9901:localhost:5901
```

```bash
$ vncviewer localhost:9901
```