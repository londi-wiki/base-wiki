---
title : 'State Machine'
date : 2023-09-25T09:32:51+02:00
tags: ["draft"]
author: "Leon"
math: false
---

## Basic state machine example

```C
#define LED 2
#define BUTTON 0

int s = 0;

void setup() {
  Serial.begin(115200);
  pinMode(LED, OUTPUT);
  pinMode(BUTTON, INPUT);
}

void loop() {
  int b = digitalRead(BUTTON);
  if (s == 0 && pressed(b)) { // s is state
    s = 1; digitalWrite(LED, HIGH); // on
    Serial.printf("state changed: %d\n", s);
  } else if (s == 1 && !pressed(b)) {
    s = 2;
    Serial.printf("state changed: %d\n", s);
  } else if (s == 2 && pressed(b)) {
    s = 3; digitalWrite(LED, LOW); // off
    Serial.printf("state changed: %d\n", s);
  } else if (s == 3 && !pressed(b)) {
    s = 0;
    Serial.printf("state changed: %d\n", s);
  } 
}

bool pressed(int value) {
  return value == HIGH;
}
```

## Extended

Only turn off LED if button is pressed more than 1s.

```C
#define LED 2
#define BUTTON 0

unsigned long myTime;

int s = 0;

void setup() {
  Serial.begin(115200);
  pinMode(LED, OUTPUT);
  pinMode(BUTTON, INPUT);
}

void loop() {
  int b = digitalRead(BUTTON);

  if (s == 0 && pressed(b)) { // s is state
    s = 1; digitalWrite(LED, HIGH); // on
    Serial.printf("state changed: %d\n", s);

  } else if (s == 1 && !pressed(b)) {
    s = 2;
    Serial.printf("state changed: %d\n", s);

  } else if (s == 2 && pressed(b)) {
    myTime = millis();
    s = 3;
    Serial.printf("state changed: %d\n", s);

  } else if (s == 3 && !pressed(b)) {
    if(millis() - myTime >= 1000l) {
      s = 4;
      Serial.printf("state changed: %d\n", s);
    } else {
      s = 2;
      myTime = 0;
    }

  } else if (s == 4) {
    s = 5; digitalWrite(LED, LOW); // off
    Serial.printf("state changed: %d\n", s);
    myTime = 0;

  } else if (s == 5 && !pressed(b)) {
    s = 0;
    Serial.printf("state changed: %d\n", s);

  } 
}

bool pressed(int value) {
  return value == HIGH;
}
```