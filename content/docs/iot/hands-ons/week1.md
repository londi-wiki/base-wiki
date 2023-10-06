---
title : 'Week1'
date : 2023-09-21T18:40:02+02:00
tags: ["week1"]
author: "Leon"
math: false
---

# Blink example

## ESP8266

```C
void setup() {
  pinMode(0, OUTPUT);
}

void loop() {
  digitalWrite(0, HIGH);
  delay(500);
  digitalWrite(0, LOW);
  delay(500);
}
```


## ESP8266

```C
#include <Arduino.h>
#include <Adafruit_TinyUSB.h> // for Serial


// the setup function runs once when you press reset or power the board
void setup() {
  // initialize digital pin LED_BUILTIN as an output.
  pinMode(LED_BUILTIN, OUTPUT);
}
     
// the loop function runs over and over again forever
void loop() {
  digitalToggle(LED_BUILTIN); // turn the LED on (HIGH is the voltage level)
  delay(1000);                // wait for a second
}
```

## NeoPixel LED Fader

```C
/**
Author: Leon Luethi
Date: 21.09.2023
Version: 1.0
*/

#include <Arduino.h>
#include <Adafruit_TinyUSB.h>
#include <Adafruit_NeoPixel.h>

int LED_PIN = PIN_NEOPIXEL;
int colorR = 255;
int colorG = 0;
int colorB = 0;

int state = 0;

Adafruit_NeoPixel rgbLed = Adafruit_NeoPixel(1, LED_PIN, NEO_GRB + NEO_KHZ800);


void setup() {
  pinMode(LED_BUILTIN, OUTPUT);
  rgbLed.begin();
  rgbLed.clear();
  rgbLed.setBrightness(10);
  rgbLed.show();
}
     
void loop() {
  //digitalToggle(LED_BUILTIN);

  rgbLed.setPixelColor(0, colorR, colorG, colorB);
  rgbLed.show();

  
  switch(state) {
    case 0:
      if(colorB < 255) {
        colorR = 255;
        colorG = 0;
        colorB += 5;
      } else {
        state += 1;
      }
      break;
    
    case 1:
      if(colorR > 0) {
        colorR -= 5;
        colorG = 0;
        colorB = 255;
      } else {
        state += 1;
      }
      break;

    case 2:
      if(colorG < 255) {
        colorR = 0;
        colorG += 5;
        colorB = 255;
      } else {
        state += 1;
      }
      break;

    case 3:
      if(colorB > 0) {
        colorR = 0;
        colorG = 255;
        colorB -= 5;
      } else {
        state += 1;
      }
      break;

    case 4:
      if(colorR < 255) {
        colorR += 5;
        colorG = 255;
        colorB = 0;
      } else {
        state += 1;
      }
      break;

    case 5:
      if(colorG > 0) {
        colorR = 255;
        colorG -= 5;
        colorB = 0;
      } else {
        state = 0;
      }
      break;
  }


  delay(50);
}
```
