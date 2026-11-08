---
title: "Adafruit GFX fork providing OLED support on mbed RTOS"
description: ""
date: "2021-06-01"
author:  "system"
showChildren: true
type: "menu_list"
githublink: "https://github.com/TcMenu/Adafruit-GFX-mbed-fork"
banner: ""
---

We maintain a fork of Adafruit_GFX that provides OLED support on a wide range of non-Arduino environments, namely ESP32-IDF, STM32Cube, PicoSDK, and mbed RTOS. It is the base display setup for outside of Arduino and is tested on all the above platforms.

The repository is hosted on GitHub [https://github.com/TcMenu/Adafruit-GFX-mbed-fork] and is tested on STM32 hardware. We have tested it with both an SPI and I2C interface.

There are two examples showing how to use this library packaged with it. It is also possible to [generate a graphical menu with this driver from tcMenu](https://github.com/TcMenu/tcMenu)

## Library History 

The library was ported from the original [AdaFruit - Adafruit_GFX repo](https://github.com/adafruit/Adafruit-GFX-Library) into the following repository [the original SSD1306 library for mbed 2](https://os.mbed.com/users/nkhorman/code/Adafruit_GFX/).

* For the core, we moved the library to always use tcUnicodeHelper to draw fonts, and made it compile outside of Arduino.
* For Framebuffers, this is new work by us.
* For SH1106 and SSD1306 OLEDs, I simplified the code to make it a bit more efficient.
* For SH1107 OLED, this is new work by us. 
