---
weight: 999
title: "Neovim"
description: ""
icon: "article"
date: "2024-02-12T17:34:11+01:00"
lastmod: "2024-02-12T17:34:11+01:00"
draft: false
toc: true
---

# Install instructions

## Install Neovim in wsl

```bash
# look for latest stable release: https://github.com/neovim/neovim/releases
wget https://github.com/neovim/neovim/releases/download/v0.9.5/nvim-linux64.tar.gz
tar -xzvf nvim-linux64.tar.gz
sudo cp -R nvim-linux64 /usr/share/
sudo ln -s /usr/share/nvim-linux64/bin/nvim /usr/bin/nvim

# test it
nvim
```

## Install lazy.vim

[lazyvim.org](https://www.lazyvim.org/installation)

```bash
git clone https://github.com/LazyVim/starter ~/.config/nvim
rm -rf ~/.config/nvim/.git

# test again
nvim
```

## Install nerdfont

This is useful to display folder/file icons in the neo-tree.

Look for a [nerdfont](https://www.nerdfonts.com/font-downloads), download and install it.

Then go to the windows termin settings > default > appearance > font and select the "mono" font of the newly installed font.

Recommendations:
- Hack nerd font
- JetBrainsMono Nerd font

## Install lazy git

[lazy-git](https://github.com/jesseduffield/lazygit?tab=readme-ov-file#installation)

```bash
LAZYGIT_VERSION=$(curl -s "https://api.github.com/repos/jesseduffield/lazygit/releases/latest" | grep -Po '"tag_name": "v\K[^"]*')
curl -Lo lazygit.tar.gz "https://github.com/jesseduffield/lazygit/releases/latest/download/lazygit_${LAZYGIT_VERSION}_Linux_x86_64.tar.gz"
tar xf lazygit.tar.gz lazygit
sudo install lazygit /usr/local/bin
```

## Fix sourcing issues (encoding)

> "Failed to source /.../neo-tree.nvim/plugin/neo-tree.vim" ... Trailing character ....

Change encoding of all vim plugin files to unix

```bash
# optional
git config --global core.autocrlf false
sudo git config --system core.autocrlf false

sudo apt install dos2unix
find /home/USER/.local/share/nvim/lazy/ -type f -name "*.vim" -exec dos2unix {} +
```
