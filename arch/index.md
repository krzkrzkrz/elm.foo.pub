# Arch Journey

[Arch](https://archlinux.org) A simple light-weight Linux distribution

## Update mirrors and packages

```shell
sudo pacmane -Syyyu
```

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


