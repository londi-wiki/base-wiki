---
weight: 999
title: "Web client"
description: ""
icon: "web"
date: "2023-10-09T08:48:26+02:00"
lastmod: "2023-10-09T08:48:26+02:00"
draft: false
toc: true
---

```bash
curl -v https://leonluethi.com/test.json
curl --data "t=23" https://postb.in/...
```

## Create a webclient

1. Create a socket
2. Connect to a remote host (e.g. Port 80)
3. Send a client request and read the server response
4. Close the connection

## Create a webserver

1. Create a server at a specific port
2. Begin listening at the local ip address on that port
3. accept connections from clients
4. read the client request and send a response
5. close the connection

```C
#include <ESP8266WiFi.h>

const char *ssid = "MY_SSID"; 
const char *password = "MY_PASSWORD";
const int port = 80;

WiFiServer server(port);

void setup() {
  Serial.begin(115200);
  Serial.print("\nConnecting to network ");
  Serial.println(ssid);
  WiFi.mode(WIFI_STA);
  WiFi.begin(ssid, password);
  while (WiFi.status() != WL_CONNECTED) {
    delay(100);
  }
  Serial.print("Connected to network, local IP = "); 
  Serial.println(WiFi.localIP());
  server.begin();
}

void loop() {
  WiFiClient client = server.available();
  if (client && client.connected()) {
    Serial.println("Connection accepted, remote IP = ");
    Serial.println(client.remoteIP());

    // Read HTTP request
    int ch = client.read();
    while (ch != -1) {
      Serial.print((char) ch);
      ch = client.read();
    }

    // Send HTTP response
    client.print("HTTP/1.1 200 OK\r\n");
    client.print("Content-Length: 9\r\n");
    client.print("Connection: close\r\n");
    client.print("\r\n");
    client.print("It works!");

    delay(1); // Give Web client time to receive data
    client.stop();
  }
}
```

## With basic autentication

[with authentication](https://github.com/tamberg/fhnw-iot/blob/master/04/Arduino/ESP8266_WebServerSecureBasicAuth/ESP8266_WebServerSecureBasicAuth.ino) to study.

`curl -v --user "LEON:BANANA" http://192.168.103.22:80`

```C
#include <ESP8266WiFi.h>

const char *ssid = "MY_SSID"; 
const char *password = "MY_PASSWORD";
// https://ddg.co/?q=base64+encode+MY_USER%3AMY_PASSWORD
const char *storedCreds = "TEVPTjpCQU5BTkE="; // LEON:BANANA
const int maxCredsLen = 64;
const int port = 80;

WiFiServer server(port);

void setup() {
  Serial.begin(115200);
  Serial.print("\nConnecting to network ");
  Serial.println(ssid);
  WiFi.mode(WIFI_STA);
  WiFi.begin(ssid, password);
  while (WiFi.status() != WL_CONNECTED) {
    delay(100);
  }
  Serial.print("Connected to network, local IP = "); 
  Serial.println(WiFi.localIP());
  server.begin();
}

void readStringToEndOfLine(WiFiClient client, char *s, int maxLen) {
  memset(s, '\0', maxLen); // fill string with '\0'
  int i = 0;
  int ch = client.read();
  while (i < (maxLen - 1) && ch != -1 && ch != '\r' && ch != '\n') {
    s[i] = ch;
    i++;
    ch = client.read();
  }
}

void send200Response(WiFiClient client) {
  client.print("HTTP/1.1 200 OK\r\n");
  client.print("Content-Length: 0\r\n");
  client.print("Connection: close\r\n");
  client.print("\r\n");
}

void send401Response(WiFiClient client) {
  client.print("HTTP/1.1 401 Unauthorized\r\n");
  client.print("WWW-Authenticate: Basic\r\n");
  client.print("Content-Length: 0\r\n");
  client.print("Connection: close\r\n");
  client.print("\r\n");
}

void loop() {
  WiFiClient client = server.available();
  if (client && client.connected()) {
    Serial.println(client.remoteIP());
    if (client.find("Authorization: Basic ")) {
      char creds[maxCredsLen];
      readStringToEndOfLine(client, creds, maxCredsLen);
      Serial.println(creds);
      client.find("\r\n\r\n"); // Ignore further request headers
      if (strcmp(storedCreds, creds) == 0) {
        send200Response(client);
      } else {
        send401Response(client);
      }
    } else {
      send401Response(client);
    }
    delay(1); // Give Web browser time to receive data
    client.stop();
  }
}
```
