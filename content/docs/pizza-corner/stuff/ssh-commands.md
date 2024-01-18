---
weight: 999
title: "ssh commands"
description: ""
icon: "article"
date: "2024-01-01T16:54:40+01:00"
lastmod: "2024-01-01T16:54:40+01:00"
draft: false
toc: true
---

## SSH hostkey entfernen

```bash
ssh-keygen -R hostname
```

## SSH Proxy

```bash
ssh -D 1337 -N -C root@IP_ADDRESS
# -D 1337: SOCKS
# -N: Not execute remote commands
# -C: Compress
```