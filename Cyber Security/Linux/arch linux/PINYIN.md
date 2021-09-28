```bash
sudo pacman -S fxitx fcitx-sunpinyin fcitx-configtool
```

In : ~/.xinitrc
```
export GTK_IM_MODULE=fcitx
export QT_IM_MODULE=fcitx
export XMODIFIERS=@im=fcitx
...
exec YOUR_WM
```