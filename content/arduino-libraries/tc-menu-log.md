---
title: "TcMenu logging framework across Arduino, PicoSDK, STM32Cube, ESP32-IDF and mbed6"
description: ""
date: "2026-08-10"
author:  "system"
showChildren: true
type: "blog"
githublink: "https://github.com/TcMenu/TcMenuLog"
referenceDocs: "/taskmanagerio/html/index.html"
banner: "/products/arduino-libraries/images/electronics/arduino/taskmgr/taskmanager-conceptual-diagram.png"
---

TcMenu logging provides standardized logging across a wide range of environments.

* Arduino - generally maps to a Serial or similar Print capable device.
* mbed6 - uses the mbed IO facilities to output the logging.
* STM32Cube - uses the standard IO channels so messages are delivered through ST-Link.
* ESP32-IDF - uses the standard IO channels so messages are delivered to the monitor.
* PicoSDK - two choices, either the tty USB channel, or stdio.

## More information about logging

