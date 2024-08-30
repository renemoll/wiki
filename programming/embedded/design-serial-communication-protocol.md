---
title: Designing a serial communication protocol
description: 
published: true
date: 2024-08-30T14:14:36.996Z
tags: 
editor: markdown
dateCreated: 2024-08-29T13:00:17.951Z
---

# Designing a serial communication protocol

Options:
* Synchronous
* Asynchronous

## Synchronous

* Transmitter and receiver are synchronised -> no need for synchronisation
* Clear start/stop/framing

## Asynchronous

* Transmitter and receiver need to be synchronised


# Links

Framing
* [Framing in serial communications](https://eli.thegreenplace.net/2009/08/12/framing-in-serial-communications)
* COBS
* Byte stuffing (like HLDC, PPP)
* https://web.cs.wpi.edu/~rek/Undergrad_Nets/B07/BitByteStuff.pdf

Reception in Python
* [Co-routines as an alternative to state machines](https://eli.thegreenplace.net/2009/08/29/co-routines-as-an-alternative-to-state-machines)
