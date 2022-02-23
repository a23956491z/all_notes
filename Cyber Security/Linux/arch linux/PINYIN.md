```bash
sudo pacman -S fxitx fcitx-sunpinyin fcitx-configtool
```
裝fcitx5-qt5-git 或 fcitx5-qt可能比較好

fcitx fcitx-qt5 fcitx-sunpinyin fcitx-configtool

In : ~/.xinitrc
```
export GTK_IM_MODULE=fcitx
export QT_IM_MODULE=fcitx
export XMODIFIERS=@im=fcitx
...
exec YOUR_WM
```


fcitx-diagnose
檢查 fcitx的功能
