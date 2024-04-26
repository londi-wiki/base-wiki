---
weight: 999
title: "Chrome linux"
description: ""
icon: "article"
date: "2024-04-26T08:34:11+01:00"
lastmod: "2024-04-26T08:34:11+01:00"
draft: false
toc: true
---

## How to install

```bash
sudo apt-get install -y libappindicator1 fonts-liberation libu2f-udev
# sudo apt --fix-broken install
wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb
sudo dpkg -i google-chrome-stable_current_amd64.deb
```