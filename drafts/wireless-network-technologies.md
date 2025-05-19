---
title: Wireless Network Technologies
description: 
published: true
date: 2025-05-19T09:44:43.957Z
tags: 
editor: markdown
dateCreated: 2025-05-14T13:05:30.088Z
---

# Wireless Network Technologies


## Scratchpad

Goal: overview of wireless communication technologies

Topics of interest
* range (LOS, NLOS)
* data rate
* power consumption indication
* number of nodes per network
* security
* Reliability / QoS
* license

Note:
* physical layer
* data link
* media access
* ... (what do different technolgies provide?)

Use-cases
* gather information (sensors, monitoring)
* signal user/machine (trigger actions, alarms)
* firmware update (OTA updates)



### Network acrhitecture

Typical LPWAN:
* Nodes connect to a gateway
  * gateway manages LPWAN network
* Gateways are connected to a (local) network server (also called base station, or core)
  * network server routes trafic and performs protocol translation 
* network server connects to application servers (i.e. cloud).

Cellular LPWAN:
* Nodes connect to a gateway, different technologies can be used next to each other
* Gateways of different technologies connect to the same network server/base station
* base station connects to cloud solution

Mixed IoT:
* Nodes connect to base station
* Gateways may be used to translate protocols or transport one protocol over another.

[Comparative analysis of ZigBee, LoRa, and NB-IoT in a smart building: advantages, limitations, and integration possibilities](https://www.researchgate.net/publication/387423926_Comparative_analysis_of_ZigBee_LoRa_and_NB-IoT_in_a_smart_building_advantages_limitations_and_integration_possibilities)


Technology | Physical | MAC | Network | Transport | Application |
| --- | --- | --- |
| BLE (802.15.1) | Y | Y | Y | Y | Y |
| IEEE 802.15.4 | Y | Y | N | N | N |
| WiFi | Y | Y | N | N | N |
| Zigbee | N | N | Y | Y | Y |
| Z-Wave | N | N | Y | Y | Y |
| IPv6 | N | N | Y | N | N |
| Thread | N | N | Y | N | N |
| TCP / UDP | N | N | N | Y | N |
| Matter | N | N | N | N | Y |

> ISA100.11a: 802.15.4 + 6LoWPAN

### local (?) area network

| Technology | BLE (802.15.1) | WiFi | IEEE 802.15.4 / Zigbee | Z-Wave
| --- | --- | --- | --- |
| Range | <100m | | 10m - 100m | 100m - 800m |
| Industry | | | Medical, Industry | Home automation |
| Frequency band | 2.4GHz | 2.4GHz, 5GHz, 6GHz | 800MHz - 900MHz,<br>2.4GHz | 800MHz - 900MHz |
| Transmission rate | 125 kbit/s - 2Mbit/s | 400kbit/s - 22Gbit/s | 250 kbit/s | 100 kbit/s |

 6LoWPAN: IPv6 over a low power network



Omitted:
* ANT: discontinued
* LiFi: requires line of sight
* MiWi: Microchip only
* NFC: due to limited range
* RFID
* WirelessHART: for (industrial) control applications

### medium (?) area network

* LTE-advanced
* 5G
* LoRa
* DASH7

### LPWAN (low-power wide area network)

| Technology | LTE-M | NB-IoT | LoRaWAN | D7AP | NB-Fi | Telensa | IEEE 802.15.4k | IEEE 802.15.4g | Weightless(-P) | 
| --- | --- | --- | --- |
| Frequency band | Licenced | Licenced | Unlicenced | Unlicenced | Unlicenced | Unlicenced | Unlicenced | Unlicenced | Unlicenced |


> Qowisio, mIoTy, RPW?


Omitted:
* EC-GSM: due to relative high power requirements
* Ingenu: due to relative high power requirements
* Sigfox: due to limited message size and messages per day (12 bytes upload, 8 bytes download, 140 messages per day [Qualification](https://build.sigfox.com/study))
* Weightless-N/W: do not seem to be available

### [Low-Power Wide-Area Networks: A Broad Overview of Its Different Aspects](https://ieeexplore.ieee.org/abstract/document/9848798)
* Low-power wide-area networks (LPWANs)

**One usefull grouping is in data rate vs range**
![Overview](https://ieeexplore.ieee.org/mediastore/IEEE/content/media/6287639/9668973/9848798/cenke2-3196182-small.gif)

Low data rate & short range
* Bluetooth
* Thread
* zigbee
* RFID
* NFC

High data rate & short range
* WiFi

High data rate & long range
* Cellular (3G/4G/5G)

Low data rate & long range
* LoRa
* Sigfox
* LTE-M
* NB-IOT
* Z-wave
* 6LoWPAN

> TODO: , DECT NR, Zigbee mesh, BLE mesh ?

**Grouping by energy efficiency**

Energy efficiency (from high to low)
* LPWAN
  * Long Range (LoRa)
  * SigFox
  * Narrowband-IoT (NB-IoT)
  * Long Term Evolution for Machines (LTE-M)
  * Ingenu
  * Telensa
  * DASH7
  * Extended Coverage Global System for Mobile Communication (EC-GSM)
  * Weightless-N
  * Weightless-P
  * Weightless-W
  * IEEE 802.15.4k
  * IEEE 802.15.4g
* WSN
  * Zigbee
  * 6LowPAN
* Short range communication
  * Bluetooth
  * WiFi
* Cellular





