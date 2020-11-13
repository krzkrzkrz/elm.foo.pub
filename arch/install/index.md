# Arch installation

[Official installation guide](https://wiki.archlinux.org/index.php/installation_guide)

Some personal notes that follow the steps on the official guide

## Verify the boot mode

If the command shows the directory without error, then the system is booted in UEFI mode

```shell
ls /sys/firmware/efi/efivars
```

## Connect to the internet via `iwct`

```shell
iwctl
[iwd]# help
[iwd]# device list
[iwd]# station wlan0 scan
[iwd]# station wlan0 get-networks
[iwd]# station wlan0 connect "How you doing?"
```

## Test internet connection

```shell
ping archlinux.org
```

## Update the system clock to ensure the system clock is accurate:

```shell
timedatectl set-ntp true
```

## Create partitions

```shell
fdisk -l
fdisk /dev/nvme0n1
```

Delete all partitions first

```shell
Command (m for help): d
```

Create a new GPT disk label

```shell
Command (m for help): g
```

Create an EFI system partition

```shell
Command (m for help): n
Partition number (1-128, default 1): <enter>
First sector (..., default 2048): <enter>
Last sector (..., default ...): +500M
Do you want to remove the signature? y

Command (m for help): t
Partition type (type L to list all types): 1
```

Create a root partition

```shell
Command (m for help): n
Partition number (1-128, default 1): <enter>
First sector (..., default 2048): <enter>
Last sector (..., default ...): <enter>
Do you want to remove the signature? y

Command (m for help): t
Partition type (type L to list all types): 20 (Linux filesystem)
```

Write the partitions

```shell
Command (m for help): w
```

## Format the EFI system partition

```shell
mkfs.fat -F32 /dev/nvme0n1p1
```

## Format the root partition

```shell
mkfs.ext4 /dev/nvme0n1p2
```

## Mount the root file systems

```shell
mount /dev/nvme0n1p2 /mnt
```

**[Dont need to do this]** Mount the EFI file systems

Since you will do this in arch-chroot anyways during the `GRUB` installation process

```shell
mkdir /mnt/boot
mount /dev/nvme0n1p1 /mnt/boot
```

## Install essential packages

```shell
pacstrap /mnt base linux linux-firmware
```

## Configure Fstab

```shell
genfstab -U /mnt >> /mnt/etc/fstab
```

## Change root into the new system:

```shell
arch-chroot /mnt
```

## Set the time zone

```shell
ln -sf /usr/share/zoneinfo/Asia/Manila /etc/localtime
```

## Run `hwclock` to generate `/etc/adjtime`:

```shell
hwclock --systohc
```

## Edit `/etc/locale.gen` and uncomment `en_US.UTF-8 UTF-8`. Generate the locales by running:

```shell
locale-gen
```

## Create the `locale.conf` file, and set the `LANG` variable accordingly:

```shell
vim /etc/locale.conf
LANG=en_US.UTF-8
```

## Create the hostname file:

```shell
vim /etc/hostname
foopub
```

## Add matching entries to hosts:

```shell
/etc/hosts
127.0.0.1 localhost
::1 localhost
127.0.1.1 foopub.localdomain myhostname
```

## Creating a new initramfs

**[Dont need to do this]** is usually not required, because mkinitcpio was run on installation of the kernel package with pacstrap.

```shell
mkinitcpio -P
```

## Set the root password

```shell
passwd
```

## Install a bootloader: GRUB

```shell
pacman -S grub efibootmgr dosfstools os-prober mtools
mkdir /boot/EFI
mount /dev/nvme0np1p1 /boot/EFI
grub-install --target=x86_64-efi --bootloader-id=grub_uefi --recheck
grub-mkconfig -o /boot/grub/grub.cfg
```

## Create a swapfile

```shell
dd if=/dev/zero of=/swapfile bs=1M count=512 status=progress
chmod 600 /swapfile
mkswap /swapfile
swapon /swapfile
```

Make sure this is inserted at the end of `/etc/fstab`

```shell
/swapfile none swap defaults 0 0
```

## Install Intel graphics card

```shell
pacman -S mesa
```

## Install Intel microcode

```shell
pacman -S intel-ucode
```

`grub-mkconfig` will automatically detect the microcode update and configure GRUB appropriately. After installing the microcode package, regenerate the GRUB config to activate loading the microcode update by running:

```shell
grub-mkconfig -o /boot/grub/grub.cfg
```

## Install `sudo`

```shell
pacman -S sudo
```

## Create a user

```shell
useradd -m -g users -G wheel chris
passwd chris
```

Give new user access to sudo command

```shell
EDITOR=vim visudo
```

Uncomment `%wheel ALL=(ALL) ALL`

## Finish up

Exit `arch-chroot`

```shell
exit
```

Unmount all the partitions with

```shell
umount -R /mnt
```

-OR-

```shell
umount -a
```

-OR- if mount still doesnt work

```shell
umount -l /mnt
```

Its ok to see get some errors here or busy status. For the most part, we are all set

Shutdown, take USB drive out and reboot

```shell
poweroff
```
