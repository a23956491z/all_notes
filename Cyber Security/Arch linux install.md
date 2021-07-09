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
`mkfs.ext4 /dev/ROOT_PARTION`