---
title: Serial communication protocol
description: 
published: true
date: 2025-02-02T21:44:24.159Z
tags: 
editor: markdown
dateCreated: 2024-08-15T19:03:53.879Z
---

# Serial communication protocol

* What is "serial"
* Refer to communication protocol
* What is available?
  Some protocols define physical/datalink/network/a whole stack



## Terminology

Term | Description
--- | ---
Network protocol | Defining network, data link and physical layer.
I<sup>2</sup>C | Inter-Integrated Circuit.
LIN | Local Interconnect Network.
SPI | Serial Peripheral Interface.
UART | Universal Asynchronous Receiver Transmitter.
USART | Universal Synchronous-Asynchronous Receiver Transmitter.
USB | Universal Serial Bus.
Multidrop bus | A bus able to connect three or more devices, including arbitration. 

### Synchronous vs asynchronous

In serial communication, the transmission and reception lines/streams can be synchronous or asynchronous. In essense, this means if the two devices synchronise theirs clocks or not.

In synchronsous communication, a clock signal is transmitted along the data to synchronise  transmitter and receiver. Each time the transmitter sends the next bit, a clock pulse is generated to signal the new bit value for the receiver to sample. Example are I<sup>2</sup>C, SPI and USART.

In asynchronsous communication, the transmitter and receiver have to agree beforehand on a common data (clock) rate and some synchronisation methods as they do not share a clock line directly. Instead, the receiver must sample the transmission line at the right time. For synchronisation, UART for example uses a start and stop bit to signal the start and end of a data frame. Examples for asynchronous busses are UART and USB.

## Protocols

Protocol | Timing | Duplex | Topology | Control
--- | --- | --- | --- | ---
CAN | Asynchronous | Half | Multi-drop | Multi-master
I2C | Synchronous | Half | Multi-drop | Multi-master
LIN | Synchronous | Half | Multi-drop | Single master
SMBus | Synchronous | Half | Multi-drop | Multi-master
SPI | Synchronous | Full, simplex | Multi-drop | Single-master
RS-485 | Asynchronous | Half | Multi-drop | Multi-master
RS-232 | Asynchronous | Full, simplex | Point to point | ?
UART | Asynchronous | RS-232/485/TTL | RS-232/485/TTL | ?

### Local Interconnect Network (LIN)

A network protocol from the automotive industry, positioned as a low-cost alternative to CAN. Commonly used in automotive for low bandwidth systems (1-20 kbit/s). A network is formed by a nodes connected to a single bus, with a single master node initiating communication.

The master initiates data transfers by quering a connected device. Only the device for which the address is a match responds. Once the transfer completes, the master continues on to the next address. There is no need for bus arbitration nor collision detection by utilizing a BREAK signal for synchronization. Data transfer is based on UART.

### Universal Asynchronous Receiver-Transmitter (UART)

Generic serial communication protocol widely available, from computer (modules) to microcontrollers, from home appliances to RADIO modules. UART provides asynchronous communication between two nodes. Communication may be simplex, half-duplex or full-duples, depending on utilized the physical layer.

UART is highly configurable, from baudrate to data frame, with numer of data/stop/parity bits, and flow control. Note that flow control can be hardware based, with two additional signals, or software based, by sending specific characters.




## References

* [Asynchronous Serial Communication: The Basics](https://itp.nyu.edu/physcomp/lessons/serial-communication-the-basics/)
* [Synchronous Serial Communication: The Basics](https://itp.nyu.edu/physcomp/lessons/synchronous-serial-communication-the-basics/)
* [Local Interconnect Network](https://en.wikipedia.org/wiki/Local_Interconnect_Network)
* [LIN Bus Explained - A Simple Intro [2023]](https://www.csselectronics.com/pages/lin-bus-protocol-intro-basics)


## Scratchpad

- [ ] CAN
- [ ] USB
- [ ] I2C
- [ ] SMBus
- [ ] SPI
- [ ] RS-485

- [ ] Which layers/functions are defined by the protocol?
 * CAN: DLL
 * LIN: PHY + DLL
 * UART: DLL over RS-232/RS-485 as PHY

- [ ] Abbr
- [ ] Tags
- [x] Sync prototols
- [ ] Async prototols
* [ ] https://en.wikibooks.org/wiki/Serial_Programming/RS-485
* [ ] https://en.wikibooks.org/wiki/Serial_Programming/Forming_Data_Packets
* [ ] https://commschamp.github.io/comms_protocols_cpp/#transport-stack


### Physical busses

Template:
 * characteristics
   * sync/async
   * wiring
 * applications
 * notable features

### Universal Synchronous and Asynchronous Receiver-Transmitter (USART)

A protocol which can be synchronous or asynchronous, depending on the configurarion. Asynchronous is descrived under UART, the remainder of this section focusees on the synchronous aspect.

In synchonous mode, the communication is half-duplex. 


* RS232/RS485/RS422

### * I<sup>2</sup>C
 * synchronous
 * Signals: data (SDA), clock (SCL), ground (GND)
### I<sup>3</sup>C
  * Improved Inter Integrated Circuit
  * Partially (?) backwards compatible
  * Higher transfer rates
  * Goal: sensor interface
  * Interrupt signalling via bus (no seperate wiring)
  * Dynamic address assignment
### SPI
 * synchronous
* CAN
  * 1Mbit/s
  * asynchronous
* USB
* EtherCat


### Protocols

Template:
 * brief description
 * applications
 * characteristics
 * notable features
 * physical protocol
 

 
* MODBUS
  * An industry standard in industrial electronics for control and data acquisition systems.
  * Supports different data transportation layers (TCP/IP, async serial (common: 232/485), token passing network)
  * Supports pre-defined and user-defined funcions
  * Defines data access (read/write) on single bit and 16 bit level
  
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