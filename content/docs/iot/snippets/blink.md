---
title : 'Blink'
date : 2023-09-25T08:58:50+02:00
tags: ["draft"]
author: "Leon"
math: false
---

## Blink example

```C
int PIN = 2;

void setup() {
  pinMode(PIN, OUTPUT);
}


void loop() {
  digitalWrite(PIN, HIGH);  // turn the LED on (HIGH is the voltage level)
  delay(1000);                      // wait for a second
  digitalWrite(PIN, LOW);   // turn the LED off by making the voltage LOW
  delay(1000);                      // wait for a second
}

```

> Before uploading: Detach the LED! Why? we don't know yet... :D
