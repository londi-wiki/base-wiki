---
weight: 999
title: "Rule Based Integration"
description: ""
icon: "article"
date: "2023-11-20T08:26:16+01:00"
lastmod: "2023-11-20T08:26:16+01:00"
draft: false
toc: true
---

## Nodered

```bash
docker run -it -p 1880:1880 -v node_red_data:/data --name mynodered nodered/node-red
```

## IFTTT

Webhook key: https://ifttt.com/maker_webhooks/settings

```bash
curl -X POST https://maker.ifttt.com/trigger/APPLET_ID/with/key/WEBHOOK_KEY -H "Content-Type: application/json"
```

## Discord webhook

```bash
curl -X POST https://discord.com/api/webhooks/...  -H "Content-Type: application/json" -d '{"content": "Hello world"}'
```

## mosquitto mqtt

```bash
cat mosquitto.conf
allow_anonymous true
listener 1883 0.0.0.0

docker run -it -d --name mos1 -p 1883:1883 -v /home/leon/tmp/mosquitto.conf:/mosquitto/config/mosquitto.conf eclipse-mosquitto

# set password
docker exec -it -u 1883 mos1 sh
mosquitto_passwd -c /mosquitto/passwd_file leon

# example
mqtt pub -t "test" -u "leon" -P "leon" -h "localhost" -m "field1=3000"
mqtt sub -t "test" -u "leon" -P "leon" -h "localhost"
```

> Note: TO connect the mqtt broker which runs in a docker container with a node-red docker instance, you have to use the wsl's ip address.
 
