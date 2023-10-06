---
title : 'Button'
date : 2023-09-25T09:19:25+02:00
tags: ["draft"]
author: "Leon"
math: false
---

```C
#define LED 2
#define BUTTON 0

void setup() {
  Serial.begin(115200);
  pinMode(LED, OUTPUT);
  pinMode(BUTTON, INPUT);
}


void loop() {
  int value = digitalRead(BUTTON);
  Serial.println(value);
  digitalWrite(LED, value);
}
```