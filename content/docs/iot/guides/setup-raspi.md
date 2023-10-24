---
weight: 999
title: "Setup Raspi"
description: ""
icon: "article"
date: "2023-10-23T09:24:36+02:00"
lastmod: "2023-10-23T09:24:36+02:00"
draft: false
toc: true
---

# Setup Pi

## Install nodejs

```bash
wget https://unofficial-builds.nodejs.org\
/download/release/v14.18.1\
/node-v14.18.1-linux-armv6l.tar.gz
tar -xzf node-v14.18.1-linux-armv6l.tar.gz
cd node-v14.18.1-linux-armv6l
sudo cp -R * /usr/local
node -v
```

## Install bluetooth, bluez

```bash
sudo apt-get update
sudo apt-get install bluetooth bluez \
libbluetooth-dev libudev-dev
npm install @abandonware/noble  # in local dir
```

### Test

```bash
sudo bluetoothctl
# [bluetooth]# scan on | scan off | help | quit
```



# Troubleshooting

## node-pre-gyp ERR! install response status 404 Not Found on

```bash
npm init

# probably execute also this command:
npm --build-from-source install bcrypt
```