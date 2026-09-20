---
title: "TcMenu - IoT ready menu designer and library for Arduino and mbed"
description: ""
date: "2017-10-11"
author:  "system"
showChildren: false
type: "menu_list"
githublink: "https://github.com/TcMenu/tcMenu"
referenceDocs: "/tcmenu/html/index.html"
banner: "/products/arduino-libraries/images/front/tcMenu-banner.png"
titleimg: "/products/arduino-libraries/images/electronics/arduino/themes/color-blue-example.jpg"
---

TcMenu is a modular, IoT ready multi level menu library for Arduino, ESP32-IDF, Pico-SDK, STM32Cube and mbed platforms supporting many input, display and IoT / remote interfaces. It makes presenting configuration, status and operational information much easier. Apache licensed and therefore safe for commercial use.

Start by [working out what information and state is to be represented](${relRef("menu-item-types.md")}) in the [Designer UI](https://designer.thecoderscorner.com). Take inspiration from the [Arduino menu examples](https://github.com/TcMenu/tcMenuLib/tree/main/examples). Then, run [Code Generator](${relRef("code-generator-and-plugins-guide.md")}) which outputs code for the selected board ready for use in an IDE.

${blockClear("left")}

## Building Embedded Menus for Arduino

Web based menu designer:

* [Start web based TcMenu Turbo designer](https://designer.thecoderscorner.com/)
* [Documentation for Web based TcMenu Turbo](${relRef("tcmenu-designer.md")})
* [Get help from the C++/Java/Flutter consultants who wrote tcMenu](https://www.thecoderscorner.com/support-services/consultancy/)

## Example embedded menu projects

We've done our best to provide examples and starters for every board and API that we support. Including examples for using menus directly on STM32Cube and PicoSDK.

* [Arduino menu examples - packaged with the library](https://github.com/TcMenu/tcMenuLib/tree/main/examples)
* [PicoSDK direct CMake examples](https://github.com/TcMenu/tcLibraryDev/tree/main/cmakeProject)
* [STM32Cube direct CMake examples](https://github.com/TcMenu/stm32-examples)
* [ESP32-IDF CMake with Arduino component](https://github.com/TcMenu/tcLibraryDev/tree/main/cmakeEsp32)
* [Java examples and starer projects](https://github.com/TcMenu/tcmenu-examples-starters)

## Using Tc menu library:

* [Guide to working with Menu Item Types](${relRef("menu-item-types.md")})
* [Code Generator and plugins guide](${relRef("code-generator-and-plugins-guide.md")}) 
* [EEPROM integration with menus](${relRef("menu-eeprom-integrations.md")})
* [Setting up IO expanders in designer](${relRef("setting-up-io-expanders-in-menu-designer.md")})
* [Authentication - securing sub-menus and remote connections](${relRef("secure-menuitem-pins-and-remotes.md")})
* [MenuManager and Menu iteration Guide](${relRef("menumanager-and-iteration.md")})
* [Writing a multi-language locale based menu](${relRef("multi-language-locale-menu.md")})
* [GitHub Repository - for source and releases](https://github.com/TcMenu/tcMenu)

## Menu library for vendor environments using CMake (non Arduino)

You can use STM32Cube, PicoSDK, and mbed without requiring the Arduino framework at all. We have example menu projects that build directly against STM32Cube and PicoSDK with highly impressive performance. Our direct support generally works via CMake using vendor-provided best practice.

See the examples section further up as it has links to the repositories for STM32Cube, PicoSDK, and ESP32-IDF.  

## Working with displays

* [Working with display renderers](${relRef("rendering-with-tcmenu-LCD-TFT-OLED.md")})
* [Creating and using TitleWidgets and bitmaps](${relRef("creating-and-using-bitmaps-menu.md")})
* [Themes, properties, grids, and card layout](${relRef("rendering-with-themes-icons-grids.md")})
* [How to define fonts within theme configuration](${relRef("using-custom-fonts-in-menu.md")})
* [Taking over the display and dashboards](${relRef("renderer-take-over-display.md")})
* [Adafruit_GFX performance extensions](${relRef("adafruit-gfx-performance-extensions.md")})

## Display plugins

* [DfRobot LCD shield driver](${relRef("dfrobot-input-display-plugin.md")})
* [LiquidCrystal / hd44780 display driver](${relRef("liquidcrystalio-hd44780-renderer-plugin.md")})
* [AdaFruit_GFX driver - ILI9341, ST7735, Nokia5110 etc](${relRef("adafruit_gfx-renderer-plugin.md")})
* [U8g2 driver - for SSD1306, SH1106 etc](${relRef("u8g2-renderer-plugin.md")})
* [SSD1306Ascii low memory driver - for SSD1306 on Uno](${relRef("ssd1306ascii-display-plugin.md")})
* [TFT_eSPI driver with double buffering](${relRef("tft_espi-renderer-plugin.md")})
* [AdaFruit_GFX CMake/PicoSDK/STM32Cube - OLED - LTDC, Framebuffer, SSD1306, SH1106](${relRef("adafruit_mbed-renderer-plugin.md")})
* [GxEPD2 driver - for Eink/EPD displays](${relRef("gx_epd-renderer-plugin.md")})
* [Customising a display driver](${relRef("customise-menu-input-display-plugin.md")})

## Theme plugins

* [OLED/Mono themes both bordered and inverse](${relRef("monochrome-themes-for-oled-5110.md")})
* [Color themes for most display sizes](${relRef("color-themes-for-all-display-sizes.md")})
* [Dark themes for most display sizes](${relRef("dark-themes-for-all-display-sizes.md")})

## Input plugins

* [Rotary encoder, buttons, or joystick](${relRef("encoder-switches-input-plugin.md")})
* [Using a matrix keyboard to control menu](${relRef("menu-control-using-matrix-keyboard.md")})
* [DfRobot analog pin keypad input](${relRef("dfrobot-input-display-plugin.md")})
* [Resistive touch screen menu integration](${relRef("resistive-touch-screen-plugin.md")})
* [XPT2046 and FT6206 touch screen menu integration](${relRef("ft6206-xt2046-touch-screen-plugin.md")})
* [Capacitive Touch-pad sensor input](${relRef("touch-pad-sensor-plugin.md")})

## Remotely controlling your menu / IoT

<img class="pull-left" src="/products/arduino-libraries/images/apps/embed-control/mainicon.png" width="120" alt="IoT control with embedCONTROL" > Our menu designer can build in IoT capabilities near automatically (on Ethernet2, UipEthernet (ENC28J60), ESP8266-WiFi, ESP32-WiFi, Bluetooth, and Serial). Allowing you to [remotely monitor and control your device using Embed Control](https://www.thecoderscorner.com/products/apps/embed-control/) with minimal effort.

However, to write your own remote monitoring, use our [Java Remote API](${relRef("tcmenu-java-api-to-arduino-remote-control.md")}), [TypeScript/JavaScript API](https://github.com/TcMenu/embedcontrolJS), [C#/DotNet API](https://github.com/TcMenu/tcmenu-dotnet-sdk), or the [Python API](https://github.com/TcMenu/tcmenu-python-api). Coming soon is a Dart API.

${blockClear("left")}

* [embedCONTROL UI documentation](https://www.thecoderscorner.com/products/apps/embed-control/)
* [Menu library remote connectivity tutorial](${relRef("menu-library-remote-connectivity.md")})
* [IoT monitoring and control using the Java API](${relRef("tcmenu-java-api-to-arduino-remote-control.md")})
* [TagVal protocol documentation](${relRef("embed-control-tagval-wire-protocol.md")})

### IoT and Remote control plugins

* [Serial driver for usb, rs232, and Bluetooth control](${relRef("serial-remote-plugin.md")})
* [Ethernet driver for Ethernet2 and Uip control](${relRef("ethernet-remote-plugin.md")})
* [WiFi driver for ESP32 and ESP8266 control](${relRef("esp-wifi-remote-plugin.md")})
* [Simhub connector for tcMenu using custom serial protocol](${relRef("simhub-connector.md")})
* [Embedded Java plugin for ethernet/WiFi remote](${relRef("embedded-java-ethernet-wifi.md")})
* [Serving up embedCONTROL in a web browser](${relRef("embedcontroljs-webserver-plugin.md")})
* [Device acts as client to remote server](${relRef("connect-to-remote-server-plugin.md")})

## Creating / building / modifying plugins

* [Creating plugins for use with TcMenu](https://github.com/TcMenu/tcMenu/tree/main/xmlPlugins)

## Archived documentation

* [TcMenu - Getting started, including video & slides](${relRef("tcmenu-overview-quick-start.md")})
* [Creating and generating menus using the CLI](${relRef("tcmenu-cli-workflow.md")})
* [Major code level differences between library versions](${relRef("major-differences-between-library-versions.md")})
