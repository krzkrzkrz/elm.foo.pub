# Arch Journey

[Arch](https://archlinux.org) A simple light-weight Linux distribution

## Update mirrors and packages

```shell
sudo pacmane -Syyyu
```

## Sudo

https://wiki.archlinux.org/index.php/Sudo

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

## Swap file

TODO

## Setup .xinitrc

TODO

## Reconfiguring keys

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

```shell
```


