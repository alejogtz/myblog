---
layout: post
title:  "Connect VSCode via ssh"
date:   2024-04-21 00:00:00 +0000
categories: Utils
---

# Installing Git UI

# Git-UI

Descripción

[Git UI](https://github.com/extrawurst/gitui) (o  gui para los cuates) es una simple terminal UI para comandos git.

Funcionalidades:

- Te permite agregar cambios del código por *chunks* de codigo al *staging area*
- Te permite hacer reset de cambios por chunks o por archivo
- Navegación con flechas y *keymap* siempre visibles desde la terminal

## Capturas

!https://github.com/extrawurst/gitui/raw/master/demo.gif

## ¿Quieres instalarlo?

**Requerimientos**

- `curl`, `tar`
- `sudo user`

```bash
curl -fsSL https://github.com/extrawurst/gitui/releases/download/v0.22.1/gitui-linux-musl.tar.gz \
  -o gitui.tar.gz && tar xvf gitui.tar.gz && rm gitui.tar.gz && mv gitui gui

chmod +x gui

sudo mv gui /usr/local/bin
```

Pruébalo!
Escribe `gui` en la terminal

```bash
gui
```