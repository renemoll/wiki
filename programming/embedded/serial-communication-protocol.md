---
title: Serial communication protocol
description: 
published: true
date: 2024-08-15T19:11:49.711Z
tags: 
editor: markdown
dateCreated: 2024-08-15T19:03:53.879Z
---

# Serial communication protocol









## Scratchpad

Busses
* UART/USART
* RS232/RS485/RS422
* I2C/I3C
* SPI
* CAN

Protocols
* MODBUS
* Local Interconnect Network
* smartcard protocol (?)
* IrDA (Infrared Data Association) SIR (?)
* ENDEC (?)

Synchronous serial communication
* Transmission/reception is synchronised
* Protocols
  * Synchronous transmit-receive (STR)
  * Binary Synchronous protocol (Bisync)
  * Digital Data Communications Message Protocol (DDCMP)

### UART & USART

USART: universal synchronous-asynchronous receiver transmitter
* Half-duplex
* Signals: TX, RX, CK (clock) (with optional XDIR - direction)
UART: universal asynchronous receiver transmitter
* Full-duplex
* Signal: TX, RX (with optional CTS/RTS/DE - clear to send/request to send/driver enable)

## References

* [USART vs. UART: What's the Difference?](https://resources.pcb.cadence.com/blog/usart-vs-uart-whats-the-difference)

 