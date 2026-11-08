---
title: "Adafruit GFX fork providing OLED support on PicoSDK/mbed/NativeCpp"
description: "Native C++ fork of Adafruit GFX for PicoSDK and mbed RTOS, providing high-performance OLED support (SSD1306, SH1106) for embedded UI projects."
date: "2021-06-01"
author:  "system"
showChildren: true
type: "menu_list"
githublink: "https://github.com/TcMenu/Adafruit-GFX-mbed-fork"
banner: ""
---

We maintain a fork of Adafruit_GFX that provides both OLED and FrameBuffer support on STM32Cube, PicoSDK, and mbed RTOS, it's based on the original work by both [AdaFruit - Adafruit_GFX repo](https://github.com/adafruit/Adafruit-GFX-Library) and [the original SSD1306 library for mbed 2](https://os.mbed.com/users/nkhorman/code/Adafruit_GFX/).

It compiles on PicoSDK, STM32Cube, ESP32-IDF, mbed RTOS 5 & 6, and should work in most environments that are supported by IoAbstraction. Currently, it supports OLED displays and framebuffers, but it is possible to add support for other displays in the future. It is near 100% compatible with Adafruit_GFX, so it should be easy to migrate existing code. It even supports the `Print` API implementing it in a compatible way to the original Adafruit_GFX library.

If you have Arduino code using a supported Adafruit Display that you're considering migrating to PicoSDK, STM32Cube, ESP32-IDF, or mbed, this library can considerably ease the transition.

The repository is hosted on GitHub [https://github.com/TcMenu/Adafruit-GFX-mbed-fork] and is tested on PicoSDK/PicoRev1, PicoSDK/PicoRev1WiFi, STM32Cube, and mbed.

If you're looking to build a UI project directly on PicoSDK, STM32, ESP32 or similar board, [we can provide support or consultancy with native toolchains](${relRef("training-support.md")})

There are two examples showing how to use this library packaged with it. It is also possible to generate a menu directly using [web based TcMenu designer](https://designer.thecoderscorner.com).

