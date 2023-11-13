---
weight: 999
title: "Dashboards"
description: ""
icon: "article"
date: "2023-11-13T08:32:13+01:00"
lastmod: "2023-11-13T08:32:13+01:00"
draft: false
toc: true
---

## Thingspeak REST

### WRITE

```bash
curl --location --request POST 'https://api.thingspeak.com/update?key=WRITE_API_KEY&field1=42'
```

### READ

```bash
curl --location 'https://api.thingspeak.com/channels/CHANNEL_ID/feed.json?key=READ_API_KEY'
```

## Thingspeak MQTT

You have to add a [thingspeak mqtt client](https://thingspeak.com/devices/mqtt) to get credentials for the following examples.

### Publish

```bash
mqtt pub -t "channels/CHANNEL_ID/publish" -i "CLIENT_ID" -u "USER_NAME" -P "PASSWORD" -h "mqtt3.thingspeak.com" -m "field1=3000"
```

### Subscribe

```bash
mqtt sub -t "channels/CHANNEL_ID/subscribe" -i "CLIENT_ID" -u "USER_NAME" -P "PASSWORD" -h "mqtt3.thingspeak.com" -m
```

## Nodejs Gluecode

[Mqtt Example](https://github.com/tamberg/fhnw-iot/blob/master/09/Nodejs/TtnToThingSpeakAdapterMqtt.js)

[REST Example](https://github.com/tamberg/fhnw-iot/blob/master/09/Nodejs/TtnToThingSpeakAdapter.js)

#### Serverless nodejs deployment with Vercel

[Selfhosted alternative to vercel](https://caprover.com/)

```bash
npm i -g vercel
```

[Examples](https://github.com/vercel/vercel/tree/main/examples)


## Influxdb

```bash
docker run --name influxdb -p 8086:8086 influxdb
```

#### Nodejs example

`export INFLUXDB_TOKEN=...`

```javascript
// get parameter from node command line
const param = process.argv[2];
console.log("param: ", param);
// assert param is of type integer
if (isNaN(param)) {
    console.log("parameter is not a number");
    process.exit(1);
}

const {InfluxDB, Point} = require('@influxdata/influxdb-client')

const token = process.env.INFLUXDB_TOKEN // get it from: export INFLUXDB_TOKEN=...
const url = 'http://localhost:8086'

const client = new InfluxDB({url, token})

let org = `leon`
let bucket = `iot`

let writeClient = client.getWriteApi(org, bucket, 'ns')

let point = new Point('measurement1')
    .tag('tagname1', 'tagvalue1')
    .intField('field1', param)


writeClient.writePoint(point)
console.log("WRITE POINT:\n", point);
console.log("flush");
writeClient.flush().then(r => console.log("flushed"));
console.log("Done, adeeee");
```

### Telegrad

Create a config file 'telegraf.conf'

```bash
[[inputs.cpu]]
[[outputs.file]]
```

Run docker:

```bash
docker run -v $PWD/telegraf.conf:/etc/telegraf/telegraf.conf:ro telegraf
```

