---
title: Serial communication protocol
description: 
published: true
date: 2024-08-15T19:03:53.879Z
tags: 
editor: markdown
dateCreated: 2024-08-15T19:03:53.879Z
---

# Serial communication protocol









## Scratchpad

Busses
* UART/USART
* I2C/I3C
* SPI
* CAN

Protocols
* MODBUS
* Local Interconnect Network
* smartcard protocol (?)
* IrDA (Infrared Data Association) SIR (?)
* ENDEC (?)

### UART & USART

USART: universal synchronous-asynchronous receiver transmitter
* Half-duplex
* Signals: TX, RX, CK (clock) (with optional XDIR - direction)
UART: universal asynchronous receiver transmitter
* Full-duplex
* Signal: TX, RX (with optional CTS/RTS/DE - clear to send/request to send/driver enable)

 