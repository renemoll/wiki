---
title: Serial communication protocol
description: 
published: true
date: 2024-08-15T19:56:07.393Z
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
* [ ] https://en.wikibooks.org/wiki/Serial_Programming/RS-485

Busses
* UART/USART
* RS232/RS485/RS422
* I2C/I3C
* SPI
* CAN
* USB
* EtherCat

Protocols
* MODBUS (RS-485 or TCP/IP)
* [Local Interconnect Network](https://en.wikipedia.org/wiki/Local_Interconnect_Network)
  * Low-cost alternative for CAN
  * UART based
  * Low speed
* smartcard protocol (?)
* IrDA (Infrared Data Association) SIR (?)
* ENDEC (?)
* DMX (RS-485)
> Too many to list -> https://en.wikipedia.org/wiki/List_of_automation_protocols
> Examples -> https://electronics.stackexchange.com/questions/69504/good-rs232-based-protocols-for-embedded-to-computer-communication


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

Asynchronous serial communication
* Protocols
  *  PPP

### UART & USART

USART: universal synchronous-asynchronous receiver transmitter
* Half-duplex
* Signals: TX, RX, CK (clock) (with optional XDIR - direction)
UART: universal asynchronous receiver transmitter
* Full-duplex
* Signal: TX, RX (with optional CTS/RTS/DE - clear to send/request to send/driver enable)

### Frame format examples

* [PCI Express 4](https://www.fpga4fun.com/PCI-Express4.html)
* [SATA vx.x?](https://perfectvips.com/datasheet/SATA-Packet-Generator.pdf)
* [Ethernet](https://www.cbtnuggets.com/blog/technology/networking/what-is-ethernet-frame-format)

## References

* [USART vs. UART: What's the Difference?](https://resources.pcb.cadence.com/blog/usart-vs-uart-whats-the-difference)
* [Synchronous serial communication](https://en.wikipedia.org/wiki/Synchronous_serial_communication)
* [Asynchronous serial communication](https://en.wikipedia.org/wiki/Asynchronous_serial_communication)