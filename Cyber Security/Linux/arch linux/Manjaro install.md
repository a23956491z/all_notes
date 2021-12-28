Pre setting:
* setting timezone


1. change mouse setting : disable acceleration
2. setting ssh:
	* export XFCE terminal theme (~/.confg/xfce4/terminal/terminalrc)
	* export VIM theme (~/.vimrc)
	* export ssh config (~/.ssh/config)
	 
	
3.	change panel setting : 
	* move primary panel to top
	* make time appears in middle of primary panel
	* make second panel shows workspace information


4. change wallpaper and lock screen:
	1. transmit backgrund file by ssh

5. Add shorcut:
	* Super + M show desktop
	* Super + L lock
	* Hold Super and left drag : move window
	* Super + T drop down terminal
	* Alt + Ctrl + T pop up new terminal
	* Super + E file manager
	* Super + B browser
	* Super + PgUp maximize

6. Configure Fish & OMF
	1. Remember also to config root's shell

7. Clone repos & obsidian
	1. install yay
	2. install obsidian-appimage by yay

8. ROFI
	1.`rofi -modi window -show window -show-icons`  Super + Tab
	
	
9. timeshift backup


10. Get fatest mirror
```
sudo pacman-mirrors --fasttrack && sudo pacman -Syyu
```