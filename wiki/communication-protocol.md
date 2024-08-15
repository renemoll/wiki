---
title: Communication protocol
description: 
published: true
date: 2024-08-15T18:46:02.409Z
tags: 
editor: markdown
dateCreated: 2024-08-11T20:35:37.394Z
---

# Communication protocol

## Background

A communication protocol defines how two entities exchange information. Entities can be physical devices or software units.

A communication protocol can be either:
* Text-based: encodes information only with human-readable characters, hence using a subset of all possible byte values.
* Binary: uses the full range of the byte to encode information.

Generally, test-based protocols are used when it is expected that a person will have to read the information exchange. Examples include  HTML, JSON and INI/TOML.

Binary protocols are not human-readable anymore and generally require fewer bytes to transmit the same amount of information. As such, they are allowing for a higher throughput.

## Terminology

Term | Description
--- | ---
Address format | Defines addressing the senders and receivers within a communication network. 
Data format | Defines how the information to exchange is packaged and which metadata is transmitted.
Flow control | A mechanism for the receiver to tell the sender it is (not) ready to receive the next message.
Maximum transmission unit (MTU) | Defines the maximum size of a single packet, information which exceeds the MTU is split into multiple packages.
Protocol Data Unit (PDU) | A single piece of information packaged by a specific protocol.
Full-duplex | Two entities can communicate simultaneously with each other.
Half-duplex | Two entities can communicate with each other, but **not simultaneously**.
Simplex | One entity can only transmit and the other can only receive.

## Common principles

Communication protocols are generally layered. This means the complete functionality is divided into one or more layers, each implementing a specific functionality.
This layering allows for flexibility in composition and simplifies the implementation. 

For example, a network router only needs to decode as much information to determine where to route an incoming packet. Since it does not need to interpret the complete payload, it only needs to know how to get to that specific information and ignore the rest. 

## OSI model

A **reference** model to provide a common basis for communication protocols.

Layer | PDU | Function
--- | --- | ---
Application | Data | Defines the communication protocol and interface.
Presentation | Data | Translation of data between application and network.
Session | Data | Manage a communication session.
Transport | Datagram | Provide reliable transmission of data.
Network | Packet | Transfer packets between nodes in a network. 
Data link | Frame | Transfer frames between two nodes within a network.
Physical | Symbol | Describes the physical characteristics of a raw bit (symbol) stream.

### Application

The application layer provides a specific functionality, this can be file exchange, web browsing or database access.

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
* Host addressing;
* Message forwarding;
* Connectionless communication.


### Datalink

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
