# Arch Journey

[Arch](https://archlinux.org) A simple light-weight Linux distribution

## Arch installation

Verify the boot mode. If the command shows the directory without error, then the system is booted in UEFI mode

```shell
ls /sys/firmware/efi/efivars
```

Connect to the internet via `iwct`

```shell
iwctl
[iwd]# help
[iwd]# device list
[iwd]# wlan0 device scan
[iwd]# wlan0 device get-networks
[iwd]# wlan0 device connect "How you doing?"
```

Test internet connection

```shell
ping archlinux.org
```

Update the system clock to ensure the system clock is accurate:

```shell
timedatectl set-ntp true
```

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
Command (m for help): d
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
Partition type (type L to list all types): 24 (Linux root (x86-64))
```

Write the partitions

```shell
Command (m for help): w
```

Format the EFI system partition

```shell
mkfs.fat -F32 /dev/nvme0n1p1
```

Format the root partition

```shell
mkfs.ext4 /dev/nvme0n1p2
```

Mount the root file systems

```shell
mount /dev/nvme0np1 /mnt
```

Mount the EFI file systems

```shell
mkdir /mnt/efi
mount /dev/nvme0np1 /mnt/efi
```

Install essential packages

```shell
pacstrap /mnt base linux linux-firmware
```

Configure Fstab

```shell
genfstab -U /mnt >> /mnt/etc/fstab
```

Change root into the new system:

```shell
arch-chroot /mnt
```

Set the time zone

```shell
ln -sf /usr/share/zoneinfo/Asia/Manila /etc/localtime
```

Run `hwclock` to generate `/etc/adjtime`:

```shell
hwclock --systohc
```

```shell
```

```shell
```


```shell
```

``





## Update mirrors and packages

```shell
sudo pacmane -Syyyu
```

## Sudo

[Sudo](https://wiki.archlinux.org/index.php/Sudo)

Allow users to execute the `sudo` command. i.e. `pacman -S vim`

```shell
sudo pacman -S sudo
```

```shell
vim etc/sudoers
```

To allow all users to execute the `sudo` command. Make sure the following is uncommented:

```
wheel ALL=(ALL) ALL
```

## AUR helper

Use an AUR helper to instal AUR packages easier


```shell
git clone https://aur.archlinux.org/yay.git
cd yay/
makepkg -sri
```

Install a package:

```shell
yay -S ttf-iosveka
```

Search for a package name

```shell
yay -Ss ttf-iosveka
```

Get more information about a package

```shell
yay -Si ttf-iosveka
```

Update all packages AUR and offical

```shell
yay -Syu
```

List all packages that require an update

```shell
yay -Pu
```

Cleaning unwanted dependencies

```shell
yay -Yc
```

To remove / uninstall package

```shell
yay -R ttf-iosveka
```

To remove / uninstall package and dependencies

```shell
yay -Rs ttf-iosveka
```



## Font scaling

Instead of modifying X's dpi settings. Just modify the font sizes for each application

## Swap file

[Swap](https://wiki.archlinux.org/index.php/Swap)

TODO

## Setup .xinitrc

TODO

## Reconfiguring keys

TODO

## Fix paste

TODO

## Install Vim

```shell
sudo pacman -S vim
```

### Python is needed for some Vim plugns to work properly:

```shell
sudo pacman -S python
```

### Configure Vim with a package manager (Plug):

```shell
curl -fLo ~/.vim/autoload/plug.vim --create-dirs \
    https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim
```

### Install xmonad

TODO

### Install FZF

```shell
sudo pacman -S fzf
```









```shell
```

