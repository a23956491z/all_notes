## Keyboard layout
**default layout is US**
avalialbe layout
`# ls /usr/share/kbd/keymaps/**/*.map.gz`

set layout
`# loadkeys de-latin1`

## Verify boot mode
without error: UEFI
does not exist: BIOS
`# ls /sys/firmware/efi/efivars`

## Internet
check interface
`ip link`

check connection
`ping archlinux.org`

## Partition
check devices
`# fdisk -l`
`# lsblk`

partition:
`# fdisk /dev/DISK`
or `# cfdisk`

### cfdisk
label:
`gpt` for disk larger than 2 TB
`dos` otherwise


### formating
format partition to Ext4
`# mkfs.ext4 /dev/ROOT_PARTITION`

init swap partition
`# mkswap /dev/SWAP_PARTITION`
enable swap
`# swapon /dev/SWAP_PARTITION`

### mount
`mount /dev/ROOT_PARTITION /mnt`


## install 
install essential package
`# pacstrap /mnt base linux linux-firmware vim networkmanager sudo`

sudo for sudo
vim for text editing
networkmanager for network manage

* subsitutre linux for other kernels
* linux-firmware can be omit in virtual machine
* container can omit both above

### configure boot
generate fstab file
`# genfstab -U /mnt >> /mnt/etc/fstab`

change root
`# arch-chroot /mnt`


## Time
check timedatectl 
`timedatectl status`

network synchronization
`# timedatectl set-ntp true`

### Timezone
list avaliable timezone
`# timedatectl list-timezones`
OR select timezone with UI 
`tzselect`

set time zone
`# ln -sf /usr/share/zoneinfo/_Region_/_City_ /etc/localtime`

apply timezone(generate /etc/adjtime)
`# hwclock --systohc`

## localization
edit `/etc/locale.gen`
uncomment `en_US.UTF-8 UTF-8` and other locale

generate locals
`locale-gen`

make local setting perminant:
`# echo "LANG=en_US.UTF_8" >> /etc/locale.conf`

* create `/etc/locale.conf`
	add `LANG=en_US.UTF_8`

make keyboard layout setting perminant
`# echo "KEYMAP=_layout_" >> /etc/vconle.conf`

create `/etc/vconle.conf`:
* add `KEYMAP=_layout_`
	e.g. `KEYMAP=de-latin1`

## Network
enable NetworkManager we installed:
`systemctl enable NetworkManager`

## create user
set root password:
`# passwd`


create user:
`useradd -m -G wheel -s /bin/bash USERNAME`
wheel is Administration group

edit sudoer
`visudo`
uncomment `%wheel ALL=(ALL) ALL`
allow wheel group be Administration

set user password:
`passwd USERNAME`

## REBOOT
`exit` or Ctrl+d

`reboot`