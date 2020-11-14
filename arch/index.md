# Arch Journey

[Arch](https://archlinux.org), a simple light-weight Linux distribution

[Installation notes](http://foo.pub/arch/install)

## Update mirrors and packages

```shell
sudo pacman -Syyyu
```

## Install Spectrwm

```shell
sudo pacman -S xorg xorg-xinit xf86-video-intel spectrwm dmenu xterm
```

Copy default spectrwm conf

```shell
cp /etc/spectrwm.conf .spectrwm.conf
```

Modify `vim .xinitrc` with

```shell
exec spectrwm
```

To run `Spectrwm`

```shell
startx
```

In Spectrwm, to open a terminal, type: `mod+shift+enter`

## Dotfile management

```shell
cd ~
git init
echo "/*" > .gitignore
git add -f .gitignore
git commit -m "add .gitignore"
git add -f .profile
git commit -m "add .profile"
```

You can also add folders you want to not be ignored to `.gitignore` with `!` at the start like this

```
!/.config
!/.config/fish
/.config/fish/fish_history
/.config/fish/fish_variables
/.config/fish/fishd.*
```

When I do a fresh install, just do `git clone https://github.com/<username>/dotfiles`

Which clones the repo into a new folder called `dotfiles`, and then move everything out of `dotfiles` into `~` (including the `.git` folder), overwriting any existing files.



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

