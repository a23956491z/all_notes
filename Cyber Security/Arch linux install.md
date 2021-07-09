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
`# pacstrap /mnt base linux linux-firmware`

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

select timezone with UI
`fzselect`