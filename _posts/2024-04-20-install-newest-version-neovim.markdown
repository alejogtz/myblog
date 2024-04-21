---
layout: post
title:  "Install neovim newest version"
date:   2024-04-21 00:00:00 +0000
categories: Utils
---

![neovim](https://i.imgur.com/w4ObsTo.png)

# Update neovim

## Via APT

Install software properties common

```
sudo apt-get install software-properties-common
```

Add oficial neovim apt repository

```
sudo add-apt-repository ppa:neovim-ppa/unstable
```

> If you experiment any gpg timeout related trouble,
> try by adding gpg keyserver manually
> ```
> gpg --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 7BB9C367
> ```

Update `apt-get` to reflect changes

```
sudo apt-get update
```

Finally install latest stable version of neovim

```
sudo apt install neovim
```


## Via snap

Type next command

```
sudo snap install nvim --classic
```