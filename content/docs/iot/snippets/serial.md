---
title : 'Serial'
date : 2023-09-25T08:42:46+02:00
tags: ["draft"]
author: "Leon"
math: false
---

## Serial printLn

```C
#include "Adafruit_TinyUSB.h"

void setup() {
  Serial.begin(115200);
}

void loop() {
  Serial.println("Hello");
  delay(500);
}
```