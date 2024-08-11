---
title: Communication protocol
description: 
published: true
date: 2024-08-11T20:38:15.967Z
tags: 
editor: markdown
dateCreated: 2024-08-11T20:35:37.394Z
---

# Communication protocol

## Background

A communication protocol defines how two entities (physical devices, software units) exchange information.

A communication protocol can be either:
* Text based: encodes information only with human readable characters. This implies using a subset of all possible byte values.
* Binary: uses the full range of the byte to encode information.

Generally, test-based protocols are used when it is expected that a person will have to read the information exchange. Examples include  HTML, JSON and INI/TOML.

Binary protocols are not human readable anymore and generally requires less bytes to transmit the same amount of information. Allowing for a higher throughput.

## Terminology

Term | Description
--- | ---
Adress format | Defines how to address the senders and receivers within a communication network. 
Data format | Defines how the information to exchange is packaged and which meta data is transmitted.
Flow control | A mechanism for the receiver to tell the sender it is (not) ready to receive the next message.
Maximum transmission unit (MTU) | Defines the maximum size of a single packet, informtion which exceeds the MTU is split into multiple packages.
Protocol Data Unit (PDU) | A single piece of information packaged by a specific protocol.
Full-duplex | Two entities can communicte simultanously with each other.
Half-duplex | Two entities can communicte  with each other, but **not simultanously**.
Simplex | One entity can only transmit and the other one can only receive.

## Common principles

Communication protocols are gennerally layered. Meaning the complete functionality is divided into one or more layers, each implementing a specific functionality.
This layering allows for flexibility in composition and simplifies the implementation. 

For example, a network router only needs to decode as much information to determine where to route an incoming packet to. Since it does not need to interpret the complete payload, it only needs to know how to get to that specific information and ignore the rest. 

## OSI model

A **reference** model to provide a common basis for communication protocols.

Layer | PDU | Function
--- | --- | ---
Application | Data | Defines the communcation protocol and interface.
Presentation | Data | Translation of data between application and network.
Session | Data | Manage a communication session.
Transport | Datagram | Provide reliable transmission of data.
Network | Packet | Transfer packets between nodes in a network. 
Data link | Frame | Transfer frames between two nodes within a network.
Physical | Symbol | Describes the physical characteristics of a raw bit (symbol) stream.

### Application

The application layer provide a specific functionality, this can be file exchange, web browsing or database access.

### Presentation

Typical functionality includes:
* Data conversion;
* Compression;
* Encryption & decryption;
* Serialisation.

### Session

Functionality includes:
* Opening and closing a communication session between two network entities;
* Authentication;
* Support for full-, half-duplex or simplex operation;
* Synchronisation.

### Transport

Can provide one or more of the following functionality:
* Segmentation
* Connection-oriented communication;
* Same order delivery;
* Error control, automatic repeat request (ARQ);
* Flow control;
* Congestion control/avoidance;
* Multiplexing.

### Network

Typical functionality includes:
* Host adressing;
* Message forwarding;
* Connectionless communication.


### Data link

Can provide one or more of the following functionality:
* Encapsulate network packets into frames;
* Frame synchronisation;
* Error control, including error checking and or automatic repeat request (ARQ);
* Flow control;
* Multiple access methods/control;
* Physical addressing;
* Packet switching;
* Packet queuing/scheduling.

### Physical

Provides the following functionality:
* Line coding (characteristics for symbol (bit) encoding/decoding);
* Flow control;
* Bit synchronisation;
* Medium access control support;
* Physical connection methods.

## References

* [Communication protocol](https://en.wikipedia.org/wiki/Communication_protocol)
* [OSI model](https://en.wikipedia.org/wiki/OSI_model)
