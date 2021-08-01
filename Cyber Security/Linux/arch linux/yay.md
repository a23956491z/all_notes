if using old pacman would produce problem

```bash
cd /tmp
pacman -S --needed git base-devel
git clone https://aur.archlinux.org/yay-git.git
cd yay
makepkg -si

```