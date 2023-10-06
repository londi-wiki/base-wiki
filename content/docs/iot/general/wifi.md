---
title : 'Wifi'
date : 2023-10-02T08:16:27+02:00
tags: ["draft"]
author: "Leon"
math: false
---

## Basic Wifi Example

Get an IP

```C
#include <ESP8266WiFi.h>

void setup() {
  Serial.begin(115200); // for debug output
  WiFi.mode(WIFI_STA); // _AP|_AP_STA|_OFF
  WiFi.begin("MY_SSID", "MY_PASSWORD"); // TODO
  while (WiFi.status() != WL_CONNECTED) {
    delay(500);
  }
  Serial.println(WiFi.localIP());
  Serial.print(WiFi.macAddress());
} 
```

## Dweet.io

`curl -vX POST "https://dweet.io/dweet/for/84:F3...?a0=123"`

`GET /get/dweets/for/84:F3...`

```C
{
  "this": "succeeded",
  "by": "getting",
  "the": "dweets",
  "with": [
    {
      "thing": "84:F3...",
      "created": "2023-10-02T06:50:48.163Z",
      "content": {}
    },
    {
      "thing": "84:F3...",
      "created": "2023-10-02T06:50:28.119Z",
      "content": {
        "a0": 123
      }
    }
  ]
}
```


### Send request to dweet.io

```C
#include <ESP8266WiFi.h>

const char *ssid = "MY_SSID"; // TODO
const char *password = "MY_PASSWORD"; // TODO

void setup() {
  Serial.begin(115200);
  Serial.print("\nConnecting to network ");
  Serial.println(ssid);
  WiFi.mode(WIFI_STA);
  WiFi.begin(ssid, password);
  while (WiFi.status() != WL_CONNECTED) {
    delay(500);
  }
  Serial.print("Connected to network, local IP = "); 
  Serial.println(WiFi.localIP());

  const char *host = "dweet.io";
  const char *path = "/dweet/for/84%3AF...?a0=999";
  const int port = 80;

  Serial.println("connecting to host..."); 
  // connect to remote host
  WiFiClient client;
  if (client.connect(host, port)) {
    Serial.println("connected");

    // send HTTP request
    client.print("GET ");
    client.print(path);
    client.print(" HTTP/1.1\r\n");
    client.print("Host: ");
    client.print(host);
    client.print("\r\n");
    client.print("Connection: close\r\n\r\n");

    Serial.println("sent request, waiting for response..."); 
    // read HTTP response
    while (client.connected() || client.available()) {
      int ch = client.read();
      while (ch >= 0) {
          Serial.print((char) ch);
          ch = client.read();
      }
    }

    Serial.println("finished. quiting"); 
  }
}

void loop() {}
```

### ThingSpeak Example

```C
#include <ESP8266WiFi.h>
#include "ThingSpeak.h" // always include thingspeak header file after other header files and custom macros
#include "DHTesp.h"


const char *ssid = "MY_SSID"; // TODO
const char *password = "MY_PASSWORD"; // TODO

const long CHANNEL_ID = 2288081;
const char *APK_KEY = "0RO...";
WiFiClient client;

float temperature = -1;
float humidity = -1;



DHTesp dht;


void setup() {
  Serial.begin(115200);
  Serial.print("\nConnecting to network ");
  Serial.println(ssid);
  WiFi.mode(WIFI_STA);
  ThingSpeak.begin(client);

  dht.setup(5, DHTesp::DHT11);
}

void loop() {
  delay(dht.getMinimumSamplingPeriod());
  humidity = dht.getHumidity();
  temperature = dht.getTemperature();

  Serial.println("temperature " + String(temperature));
  Serial.println("humidity " + String(humidity));

  ThingSpeak.setField(1, temperature);
  ThingSpeak.setField(2, humidity);
  ThingSpeak.setStatus("up and running");

  if(WiFi.status() != WL_CONNECTED){
    Serial.print("Attempting to connect to SSID: ");
    Serial.println(ssid);
    while(WiFi.status() != WL_CONNECTED){
      WiFi.begin(ssid, password);  // Connect to WPA/WPA2 network. Change this line if using open or WEP network
      Serial.print(".");
      delay(5000);     
    } 
    Serial.println("\nConnected.");
  }

  bool result = writeFields();

  delay(60 * 1000); // There is a limit on the request endpoint
}

bool writeFields() {
  if(WiFi.status() == WL_CONNECTED){
    int x = ThingSpeak.writeFields(CHANNEL_ID, APK_KEY);
    if(x >= 200 and x < 300){
      Serial.println("Channel update successful. httpcode: " + String(x));
      return true;
    } else {
      Serial.println("Problem updating channel. HTTP error code " + String(x));
      return false;
    }
  }
  return false;
}

```