---
weight: 999
title: "Docker"
description: ""
icon: "article"
date: "2024-01-02T23:31:53+01:00"
lastmod: "2024-01-02T23:31:53+01:00"
draft: false
toc: true
---

## Install docker on ubuntu 20.04

```bash
sudo apt update

sudo apt install apt-transport-https ca-certificates curl software-properties-common

curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -

sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu focal stable"

# check if docker-ce is now available
apt-cache policy docker-ce

sudo apt install docker-ce

sudo systemctl status docker
```

## Executing the Docker Command Without Sudo (Optional)

```bash
sudo usermod -aG docker ${USER}

# apply
su - ${USER}

# check
groups
```

## Install docker compose on ubuntu 20.04

Find latest releases: [github releases](https://github.com/docker/compose/releases)

```bash
sudo curl -L "https://github.com/docker/compose/releases/download/v2.23.3/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose

sudo chmod +x /usr/local/bin/docker-compose

docker-compose --version
```

## Selfhosted registry

## Setup

Registry with simple UI: [Joxit/docker-registry-ui](https://github.com/Joxit/docker-registry-ui)

### Add insecure-registries option

**Ubuntu**

add the file /etc/docker/daemon.json with the following content:

```bash
nano /etc/docker/daemon.json

#

{
    "insecure-registries" : [ "IP:5000" ]
}

#

sudo systemctl restart docker
```

**Docker Desktop (Windows)**

```bash
"insecure-registries": [
    "localhost:5000",
    "IP:5000",
    ...
]
```

### build and push

```bash
docker build -t APP:latest .

docker login IP:5000 -u USER -p 'PASSWORD'

docker tag APP:latest IP:5000/author/APP

docker push IP:5000/author/APP
```
