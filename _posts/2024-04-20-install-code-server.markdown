---
layout: post
title:  "Install code-server"
date:   2024-04-20 00:00:00 +0000
categories: Utils
---

# Code Server

One alternative to connect vscode with remote linux instance via ssh is install vscode standalone web server

# Installing code-server


### 1. Install from source

```bash
curl -fsSL https://code-server.dev/install.sh | sh
```

### 2. Type `code-server` to generate configuration file and stop it with `Ctrl + c`

```bash
code-server
```

- When you type `code-server`, `~/.config/code-server/config.yaml` file will be generated atuomatically

### 3. Replace local ip by public ip

```bash
sed -i 's/bind-addr: 127.0.0.1:8080/bind-addr: 0.0.0.0:8085/g' $HOME/.config/code-server/config.yaml
```

### 4. Run code-server and code it

```bash
code-server --port 8085
```

**Navigate to public IP and open in port 8085**

> You can get your current IP with next command: `curl -sSL ifconfig.me`
> 

> open chrome on: e.g. http://<your_ip>:8085
> 

### 5. show password to login

```bash
cat $HOME/.config/code-server/config.yaml
```

## SSL Configuration

### Generate self-signed certificate

```bash
openssl req -newkey rsa:2048 -nodes -keyout $HOME/.config/code-server/key.pem \
	-x509 -days 365 \
	-subj "/C=MX/ST=Oaxaca/L=Oaxaca/O=Auditore IT/OU=Inc/CN=auditore.domain.com" \
	-out $HOME/.config/code-server/cert.pem

```

### Remove useless cert lines

```bash
sed -i '/^cert:/d' ~/.config/code-server/config.yaml
sed -i '/^cert-key:/d' ~/.config/code-server/config.yaml

```

### Update cert-lines with own self-signed cert

```bash
echo "cert: $HOME/.config/code-server/cert.pem" >> ~/.config/code-server/config.yaml
echo "cert-key: $HOME/.config/code-server/key.pem" >> ~/.config/code-server/config.yaml
```

### Run code-server and navigate to start coding

```bash
code-server --port 8085 #### With SSL
```
