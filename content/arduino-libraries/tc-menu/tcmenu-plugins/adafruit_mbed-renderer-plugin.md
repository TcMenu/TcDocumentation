+++
title = "Using the Adafruit_GFX fork for STM32Cube, PicoSDK and mbed"
description = ""
tags = "display-driver, embedded-menu, menu-plugin"
type = "blog"
date = "2020-09-10"
author =  "dave"
menu = "tcmenu-plugins"
banner = "/products/arduino-libraries/images/electronics/arduino/tcMenu/oled-display.jpg"
titleimg = "/products/arduino-libraries/images/electronics/arduino/tcMenu/oled-display.jpg"
githublink = "https://github.com/TcMenu/tcMenu"
referenceDocs = "/tcmenu/html/index.html"
weight = 50
toc_needed = true
aliases = ['/products/arduino-libraries/tc-menu/using-adafruit_gfx-rendering/']
+++

In this guide we show how to use our [Adafruit_GFX port for STM32Cube/PicoSDK/mbed](https://github.com/TcMenu/Adafruit-GFX-mbed-fork) to renderer menu items with tcMenu. This rendering driver for Adafruit_GFX is built into the core menu designer, meaning it's available out of the box when either mbed, PicoSDK or STM32Cube are selected.

This fork of Adafruit_GFX library supports the following displays.

* OLED: SSD1306/SH1106 monochrome displays with a memory buffer. Both SPI and I2C are supported.
* LTDC: STM32Cube LTDC displays with a memory mapped frame buffer.
* Framebuffer: A general purpose framebuffer that can be specialized to other cases.

If you follow the instructions in either the [PicoSDK examples](https://github.com/TcMenu/tcLibraryDev/tree/main/cmakeProject), or the [STM32Cube examples](https://github.com/TcMenu/stm32-examples) they include setting up this library. Given that this library is a fork of Adafruit_GFX, it is therefore nearly 100% compatible with it. As such you can consult the [Adafruit_GFX library documentation](https://learn.adafruit.com/adafruit-gfx-graphics-library/overview) if you're not familiar with the library already.

Related documentation:
 
* [Core menu rendering class guide](${relRef("rendering-with-tcmenu-LCD-TFT-OLED.md")})
* [How to take over the display](${relRef("renderer-take-over-display.md")})
* [Our AdafruitGFX extensions improving performance](adafruit-gfx-performance-extensions.md)

## Plugin and Library details

* Library required: https://github.com/TcMenu/Adafruit-GFX-mbed-fork
* What we've tested: STM32Cube, PicoSDK, mbed 6

## Options for framebuffers such as LTDC

* Width and height represent the width and height of the framebuffer
* Memory location is the address in memory of the framebuffer's memory
* Y is inverted if this property is true

## Options for OLED displays such as SSD1306 and SH1106

* Bus type - either I2C or SPI
* Serial Bus - the bus variable of the wire type for the platform 
* Display I2C address for I2C cases
* RESET, CS and RS pins for SPI cases
* SPI Frequency, the frequency of the SPI bus (not always supported)
* Text Encoding, the encoding of the text, either UTF8 or ASCII

## General options for all displays

* Rotation. The rotation of the display between 0 and 3, 0 is not rotated
* Display variable and type. The name and type of the display variable
* Updates per second. How many times the menu structure should be scanned for changes and redrawn if needed. TcMenu tries to minimise redraws where reasonably possible.

[Back to tcMenu main page](${relRef("tc-menu")}) 
