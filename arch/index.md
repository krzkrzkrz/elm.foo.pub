# Arch Journey

[Arch](https://archlinux.org) A simple light-weight Linux distribution

[Installation notes](http://foo.pub/arch/install)

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

