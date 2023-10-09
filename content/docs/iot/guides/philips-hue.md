---
weight: 999
title: "Philips Hue"
description: ""
icon: "article"
date: "2023-10-09T09:13:11+02:00"
lastmod: "2023-10-09T09:13:11+02:00"
draft: false
toc: true
---

## API

[Philips Hue API](https://developers.meethue.com/develop/hue-api/)

[Philips Hue API 2](https://developers.meethue.com/develop/hue-api-v2/)


## Get new api user

[Getting started](https://developers.meethue.com/develop/get-started-2/)

1. Visit https://<bridge ip address>/debug/clip.html
2. Press the link button on the bridge and send the following request:
   > URL	/api
   > 
   > Body	{"devicetype":"my_hue_app#api test"}
   > 
   > Method	POST
3. After that you can test the api:
   > Address	https://<bridge ip address>/api/<USERNAME_ID>/lights
   > 
   > Method	GET


## API Examples

**Get all lights**

```bash
Address	https://<bridge ip address>/api/<USERNAME_ID>/lights
Method	GET
```

**Get a specific light**

```bash
Address	https://<bridge ip address>/api/<USERNAME_ID>/lights/1
Method	GET
```

**Switch state**

```bash
Address	https://<bridge ip address>/api/<USERNAME_ID>/lights/1/state
Body	{"on":false}
Method	PUT
```



