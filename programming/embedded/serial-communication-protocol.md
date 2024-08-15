---
title: Serial communication protocol
description: 
published: true
date: 2024-08-15T19:16:45.910Z
tags: 
editor: markdown
dateCreated: 2024-08-15T19:03:53.879Z
---

# Serial communication protocol









## Scratchpad

- [ ] Abbr
- [ ] Tags
- [x] Sync prototols
- [ ] Async prototols

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
  * Byte-oriented
    * Synchronous transmit-receive (STR)
    * Binary Synchronous protocol (Bisync)
    * Digital Data Communications Message Protocol (DDCMP)
  * Bit-oriented
    * Synchronous Data Link Control (SDLC)
    * High-Level Data Link Control (HDLC)
    * Logical Link Control (LLC)—IEEE 802.2
    * Advanced Data Communication Control Procedures (ADCCP)

### UART & USART

USART: universal synchronous-asynchronous receiver transmitter
* Half-duplex
* Signals: TX, RX, CK (clock) (with optional XDIR - direction)
UART: universal asynchronous receiver transmitter
* Full-duplex
* Signal: TX, RX (with optional CTS/RTS/DE - clear to send/request to send/driver enable)

## References

* [USART vs. UART: What's the Difference?](https://resources.pcb.cadence.com/blog/usart-vs-uart-whats-the-difference)
* [Synchronous serial communication](https://en.wikipedia.org/wiki/Synchronous_serial_communication)
 