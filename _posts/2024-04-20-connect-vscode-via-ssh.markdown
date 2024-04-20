---
layout: post
title:  "Connect VSCode via ssh"
date:   2024-04-20 00:00:00 +0000
categories: Utils
---

# Connect VSCode with cloud9 via ssh

### Cloud 9 cli

```jsx
npm install -g c9
echo "alias c=c9" >> ~/.bashrc
```

### GitUI

```jsx
curl -fsSL https://github.com/extrawurst/gitui/releases/download/v0.22.1/gitui-linux-musl.tar.gz -o gitui.tar.gz
    tar xvf gitui.tar.gz && rm gitui.tar.gz && mv gitui gui

chmod +x gui

sudo mv gui /usr/local/bin
```

### RipGrep & Fuzzy finder

```jsx
curl -LO https://github.com/BurntSushi/ripgrep/releases/download/13.0.0/ripgrep_13.0.0_amd64.deb
sudo dpkg -i ripgrep_13.0.0_amd64.deb

export FZF_CTRL_T_OPTS='-i'
export FZF_DEFAULT_COMMAND='rg --files --follow --no-ignore-vcs --hidden -g "!{node_modules/*,.git/*}"'                                                                
export FZF_CTRL_T_COMMAND="$FZF_DEFAULT_COMMAND"

git clone --depth 1 https://github.com/junegunn/fzf.git ~/.fzf
~/.fzf/install

echo "bind -x '\"\\C-h\": fzf-file-widget'" >> ~/.bash_profile
```

### Extras

```jsx
# File ~/.bashrc

# git log show with fzf
# source: https://gist.github.com/junegunn/f4fca918e937e6bf5bad
#         https://gist.github.com/junegunn/f4fca918e937e6bf5bad?permalink_comment_id=2981199#gistcomment-298119
gli()
{
  git log -15 --first-parent  --graph --color=always --format="%C(auto)%h%d %s %C(black)%C(bold)%cr" $1 | \
   fzf --ansi --no-sort --reverse --tiebreak=index --preview \
   'f() { set -- $(echo -- "$@" | grep -o "[a-f0-9]\{7\}"); [ $# -eq 0 ] || git show --color=always $1 ; }; f {}' \
   --bind "j:down,k:up,alt-j:preview-down,alt-k:preview-up,ctrl-f:preview-page-down,ctrl-b:preview-page-up,q:abort,right:execute:
                (grep -o '[a-f0-9]\{7\}' | head -1 |
                xargs -I % sh -c 'git show --color=always % | less -R') << 'FZF-EOF'
                {}
FZF-EOF" --preview-window=right:60%
}

gls()
{
  git stash list -n 5 --format="%gd %Cgreen%<(60,trunc)%gs%Creset" | \
   fzf --ansi --no-sort --reverse --tiebreak=index --preview \
   'f() { set -- $(echo -- "$@" | grep -o "stash@{[0-9]}"); [ $# -eq 0 ] || git -c color.ui=always stash show -p $1 ; }; f {}' \
   --bind "j:down,k:up,alt-j:preview-down,alt-k:preview-up,ctrl-f:preview-page-down,ctrl-b:preview-page-up,q:abort,right:execute:
                (grep -o 'stash@{[0-9]}' | head -1 |
                xargs -I % sh -c 'git -c color.ui=always stash show -p % | less -R') << 'FZF-EOF'
                {}
FZF-EOF" --preview-window=right:60%
}

source ~/.bashrc
```

### VSCode with SSH

```jsx
c ~/.ssh/authorized_keys

curl ifconfig.me
```

```jsx
Host AraFront
    HostName 54.193.70.48
    User ubuntu
    IdentityFile ~/.ssh/id_rsa

Host KudosApp
    HostName 54.200.192.76
    User ubuntu
    IdentityFile ~/.ssh/id_rsa
   

Host alejo-nexu-back
 HostName 54.177.56.155
 User ubuntu
 IdentityFile ~/.ssh/id_rsa

Host alejo-nexu-front
 HostName 50.18.232.71
 User ubuntu
 IdentityFile ~/.ssh/id_rsa

Host KevFront
 HostName 13.57.212.131
 User ubuntu
 IdentityFile ~/.ssh/id_rsa
```

**SSH Remote Extension**
