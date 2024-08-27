---
title: Digital clock
description: 
published: true
date: 2024-08-27T20:51:12.949Z
tags: 
editor: markdown
dateCreated: 2024-08-26T20:39:35.438Z
---

# Digital clock

## Requirements

* Want to place it anywhere I want, without a cable.
* The clock needs to synchronise automatically.
* Wooden housing
* Clock - digital - amber

## Design

* Battery powered
  * Type?
  * Required energy?
  * Rechargable?
  * USB rechargable?
* Automatic time
  * DCF77
    * or french alternative?
    * Or UK -> MSF 
  * WiFi -> NTP
  * Matter? / Hue?
* Display
  * 4 x 7 segment display
    * white or amber/yellow
    * size ?
  * Nixie tube?
    * IN-12 -> https://tubes-store.com/product_info.php?cPath=32_43&products_id=38
    * IV-22 -> https://tubes-store.com/product_info.php?cPath=32_44&products_id=35
    * ILC7-4/7 VFD tube  -> https://tubes-store.com/product_info.php?cPath=32_44&products_id=1374
    * dot?
* Dimmable
  * depend on ambient light?

# Scratchpad

* https://blog.blinkenlight.net/experiments/dcf77/

# 7 segment 

Available part of demo setup
* SC10-21HWA
  * 25mm
  * Common cathode
  * max 25mA (max peak 150mA for <10us)
  * forward voltage: 2V, reverse voltage 5V
* HEF4511B
  * 8 segments, one digit
  * max 25mA (per output?)
  * Given 5V supply, output is typical 4.4V
* 2N3904
  * NPN transistor, max 200mA , max 6V Vbe

R = (4.4V - 2V) / 10mA -> 240Ohm
R = (4.4V - 2V) / 20mA -> 120Ohm

Interesting
*  MAX7219 (SPI interface)
  * 8 segments + DP for 8 digits