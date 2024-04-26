---
weight: 999
title: "Proxy Server"
description: ""
icon: "article"
date: "2024-04-26T08:34:11+01:00"
lastmod: "2024-04-26T08:34:11+01:00"
draft: false
toc: true
---

[stackoverflow](https://stackoverflow.com/questions/33703965/how-can-i-run-a-spring-boot-application-on-port-80)

## Proxy Server

If you want to serve e.g. spring boot on port 80 which is running on port 8080.

```bash
sudo apt-get install apache2

a2enmod proxy
a2enmod proxy_http   

cd /etc/apache2/sites-enabled
sudo nano 000-default.conf
```

```bash
<VIRTUALHOST *:80>

    ProxyPreserveHost On

    # ...

    ProxyPass / http://localhost:8080/
</VIRTUALHOST>
```


```bash
sudo service apache2 restart
```