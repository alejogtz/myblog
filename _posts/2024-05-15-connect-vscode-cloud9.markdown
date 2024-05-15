---
layout: post
title:  "Connect VSCode with Cloud9"
date:   2024-05-15 00:00:00 +0000
categories: Tutorials
---

# Connect VSCode with Cloud9 vía SSH

## Prerequisites
- [x] VSCode
- [x] [Remote - SSH](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-ssh)
- [x] [Remote - SSH: Editing Configuration Files](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-ssh-edit)
- [x] [Remote Explorer](https://marketplace.visualstudio.com/items?itemName=ms-vscode.remote-explorer)


## Configuration

### Config Local machine 💻

#### Create ssh key-pair

- **Install recommendes addons**

![Imagen](https://i.imgur.com/TgVd7XZ.png)

- **Generate ssh key-pair**

```sh
ssh-keygen
ls -al ~/.ssh
eval `ssh-agent`
ssh-add ~/.ssh/id_rsa
cat ~/.ssh/id_rsa.pub
```

- **In remote host follow steps to add public key to `~/.ssh/authorized_keys` file**

- **Test remote ssh connection**

```sh
ssh ubuntu@54.177.56.155 -i ~/.ssh/id_rsa
```


### Config Cloud9 or any other remote instance ☁️

- Edit `~/.ssh/authorized_keys`. For example with vim o cloud0 directly

```
vi ~/.ssh/authorized_keys
# or
c9 ~/.ssh/authorized_keys # to open in cloud9 directly
```

**From  local machine copy content from `~/.ssh/id_rsa`**

```sh
cat ~/.ssh/id_rsa.pub
```

and add content at the end of `~/.ssh/authorized_keys` file

it should look seems like this

![](https://i.imgur.com/gnTlrho.png)


### Connect VSCode with cloud9 vía ssh

- **Edit `~\.ssh\config`**

![](https://i.imgur.com/l75lBco.png)

![](https://i.imgur.com/hLSe32v.png)

![](https://i.imgur.com/HgJJjy6.png)


- Add new entry for remote host following next template

```
Host {{entry_name}}
    HostName {{remote-ip or hostname}}
    User {{username}}
    IdentityFile {{path/to/rsa private key}}
```

for example:

```
Host KudosApp
    HostName 189.250.172.116
    User ubuntu
    IdentityFile ~/.ssh/id_rsa
```

- **Finally, connect vscode directly with your remote instance**

Refresh list

![](https://i.imgur.com/R70Cezi.png)

![](https://i.imgur.com/Jzpo79x.png)

![](https://i.imgur.com/Zj4INHT.png)

![](https://i.imgur.com/C7ZqoUH.png)

![](https://i.imgur.com/28lZOt9.png)

![](https://i.imgur.com/qky7vu3.png)



