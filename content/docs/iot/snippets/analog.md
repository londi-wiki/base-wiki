---
title : 'Analog'
date : 2023-09-25T09:40:04+02:00
tags: ["draft"]
author: "Leon"
math: false
---

```C
void setup() {
  Serial.begin(9600);
}

void loop() {
  int sensorValue = analogRead(A0);
  Serial.println(sensorValue);
  delay(1);
}
```
