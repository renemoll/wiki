---
title: Serial communication protocol
description: 
published: true
date: 2024-08-16T13:42:06.709Z
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
* [ ] https://en.wikibooks.org/wiki/Serial_Programming/Forming_Data_Packets
* [ ] https://commschamp.github.io/comms_protocols_cpp/#transport-stack

Busses
* UART/USART
* RS232/RS485/RS422
* I2C/I3C
* SPI
* CAN
* USB
* EtherCat

Protocols
* [Local Interconnect Network](https://en.wikipedia.org/wiki/Local_Interconnect_Network)
  * Network protocol
  * Low-cost alternative for CAN
  * UART based
  * Low speed
* MODBUS (RS-485 or TCP/IP)
* smartcard protocol (?)
* IrDA (Infrared Data Association) SIR (?)
* ENDEC (?)
* DMX (RS-485)
* NMEA 2000
> Too many to list -> https://en.wikipedia.org/wiki/List_of_automation_protocols
> Examples -> https://en.wikipedia.org/wiki/Serial_communication#Examples_of_architectures
> Examples -> https://electronics.stackexchange.com/questions/69504/good-rs232-based-protocols-for-embedded-to-computer-communication
> https://datatracker.ietf.org/doc/html/rfc935
* [rosserial](https://wiki.ros.org/rosserial)

Synchronous serial communication
* Transmission/reception is synchronised
* Protocols
  * Byte-oriented
    * Synchronous transmit-receive (STR)
    * Binary Synchronous protocol (Bisync)
    * Digital Data Communications Message Protocol (DDCMP)
  * Bit-oriented
    * Synchronous Data Link Control (SDLC) -> see HDLC (related)
    * High-Level Data Link Control (HDLC)
    * Logical Link Control (LLC)—IEEE 802.2
    * Advanced Data Communication Control Procedures (ADCCP) -> see HDLC (related).

Asynchronous serial communication
* Protocols
  * High-Level Data Link Control (HDLC)
  * PPP -> HDLC inspired
  * Digital Data Communications Message Protocol (DDCMP)
* Framing : COBS (https://en.wikipedia.org/wiki/Consistent_Overhead_Byte_Stuffing)
> [Overview of different encapsulation technologies](https://www.ieee802.org/3/efm/public/jul02/copper/oksman_copper_1_0702.pdf)




### UART & USART

USART: universal synchronous-asynchronous receiver transmitter
* Half-duplex
* Signals: TX, RX, CK (clock) (with optional XDIR - direction)
UART: universal asynchronous receiver transmitter
* Full-duplex
* Signal: TX, RX (with optional CTS/RTS/DE - clear to send/request to send/driver enable)


### High-Level Data Link Control (HDLC)

Can be used in synchronsous (bit-oriented) and asynchronous mode (byte-oriented). This will focus on asynchronous mode.
* Used for point-to-point communicaiton (can also do mutlipoint).
* 2 control bytes (SOF=EOF & escape)
* Structure: SOF (1) - ADDR (1+) - CTRL (1 or 2) - DATA (n) - CHCK (2 or 4) - EOF (1) => overhead of 6-9 bytes
  > Note that ADDR is not optional (even in PPP communication)
* Control defines 3 types of packets: information (data), supervisory (flow/error control) and unnumbered (link management).

> expand on goal & features

### Digital Data Communications Message Protocol (DDCMP)

* synchronous and asynchronous mode
* point-to-point and multipoint modes

> expand on goal & features
> https://web.archive.org/web/20110716052605/http://telecom.tbi.net/ddcmp.txt
> https://web.archive.org/web/20150909234334/http://telecom.tbi.net/ddcmp.htm

### Frame format examples

* [PCI Express 4](https://www.fpga4fun.com/PCI-Express4.html)
* [SATA vx.x?](https://perfectvips.com/datasheet/SATA-Packet-Generator.pdf)
* [Ethernet](https://www.cbtnuggets.com/blog/technology/networking/what-is-ethernet-frame-format)

## References

* [USART vs. UART: What's the Difference?](https://resources.pcb.cadence.com/blog/usart-vs-uart-whats-the-difference)
* [Synchronous serial communication](https://en.wikipedia.org/wiki/Synchronous_serial_communication)
* [Asynchronous serial communication](https://en.wikipedia.org/wiki/Asynchronous_serial_communication)
* [High-Level Data Link Control](https://en.wikipedia.org/wiki/High-Level_Data_Link_Control)