---
layout: post
title:  "Install Bare repository"
date:   2024-04-20 00:00:00 +0000
categories: Utils
---

# Manage dotfiles with a git bare repository

Bare repositories allow you to manage dotfiles with git from diference sources in your computer and sync with other machines.

We have two scenarios, first and it's neccessary do one time is create the bare repository. Once you have your github repo, you only need clone your repo in another machine


# First scenario. Create bare repository

Create bare repository in `$HOME` folder

```bash
% git init --bare $HOME/.cfg
```

In order to manipulate this repository we create an alias to point this repo.

```bash
alias config='/usr/bin/git --git-dir=$HOME/.cfg/ --work-tree=$HOME'
```

Now you can execute this command to ignore all files which no are tracked by our bare repository

```bash
config config --local status.showUntrackedFiles no
```

You can save this alias in you bash config to permanently have access

```
# File: ~/.bashrc 
#
# Add this line to your .bashrc config file
echo "alias config='/usr/bin/git --git-dir=$HOME/.cfg/ --work-tree=$HOME'" >> $HOME/.bashrc
echo "alias conf='/usr/bin/git --git-dir=$HOME/.cfg/ --work-tree=$HOME'" >> $HOME/.bashrc
```


Once you have created your repo
Now you can add config files to your bare repository

```bash
% cd $HOME/

% config status
% config add .bashrc
% config commit -m "Add bashrc"
% config add .bash_aliases
% config commit -m "Add bashrc"
% config add .gitconfig
% config commit -m "Add bashrc"

% config add .vimrc
% config commit -m "Add vimrc"
```

### Publish to github remote repository

Create openssl secret key-pair

```
% ssh-keygen
% ls -al ~/.ssh
% eval `ssh-agent`
% cat ~/.ssh/id_rsa.pub
```

Copy content displayed and add to your [github keys](https://github.com/settings/keys)

### Add config remote

Create new repository and add remote at your remotes list

```bash
config remote add <name> <url>
config remote add origin git@github.com:alejogtz/configs.git
```

Now you can publish and save your dotfiles 

```bash
% config push origin master
```



Bare repositories allow you to save dotfiles and manage with github

## Clone bare repository into another instance

```bash
% git rm --cached <file>
```

```bash
git clone --bare git@github.com:alejogtz/configs.git ~/.cfg
```

```
alias conf='/usr/bin/git --git-dir=$HOME/.cfg/ --work-tree=$HOME'
```



conf checkout


conf config --local status.showUntrackedFiles no