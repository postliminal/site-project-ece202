---
title: "Design"
date: 2021-11-01T01:26:43-07:00
draft: true
comments: false
ShowReadingTime: true
searchHidden: true
weight: 5
---

<!-- # System Design -->

[image 1] - should be showing 3 beacons, a central device, and maybe a PC? Plus X-Y coordinates and roughly spatial distance. DO NOT INCLUDE specific ble or openthread specs/terms/concepts.


# Contents

- Hardware Platforms
- Software Stack
- BLE Application
- OpenThread Application
- Location from RSSI
- Experiments


# The Hardware Platform

### The SoC: Nordic nRF52840

[images of boards?]

- (2x) Arduino Nano Sense 33 BLE
- (2x) nRF52840 Dongle
- (1x) nRF52840 Development Kit

# The Software Stack

### Embedded Software Development:
- Segger Embedded Studio
- nRF5 SDK & nRF5 SDK for Thread and Zigbee
- nRF Connect+Programmer for flashing code
- CMSIS Libraries for Arm Cortex M microcontrollers
<!-- - (... Tensorflow?) -->

### Utilities and Other tools:
- Python + Matplotlib
- nRF BLE Sniffer
- nRF 802.15.4 Sniffer
- WireShark

# BLE Application

[Cite the 5.0 specification, 2 other papers, and nordic site]

The Bluetooth specification provides a full stack solution for communication. Therefore, we don't need anything else to create the solution.

[Figure of 37+3 adv channels and next to it overlay with wifi channels to show less interference in adv channels]

### Advertising

By default occurs over channels 37, 38 and 39, which are spread out over the 2.4MHz band, and are precisely located at the edges of the wifi band to help reduce wifi interference. 

With the nordic SDK, advertisements can be precisely configured with various settings. We'll explore the use of the following:
- Window size
- RSSI dB filtering
- Advertising interval

### RSSI

Received Signal Strength Indicator. This value measures the received signal strength in dB and can be used to esitmate the distance of the receiver from the transmitter device. 

The RSSI is represented using a byte inside of the manufacturer specific data. 

# Thread Application

[Cite the openthread website, 2 other papers, and nordic site]

The 802.15.4 provides the lower layers of communication. Thread stands on top of those physical layers and implements UDP, IP Routing and 6LoWPAN. 

Attempt 1: communicate RSSI based on hardware layer functions.

Attempt 2: UDP packets

Attempt 3: use mqtt-sn 

### RSSI

### MQTT and MQTT-SN

In orderz
MQTT-SN is a variation of the MQTT protocol for Sensor Networks. 


# Location from RSSI
## Initial Model: Geomtrical Solution

- Trilateration

## Improving the Model: SVM

### Deploying the updated model: CMSIS Libraries
[How to implement SVM with CMSIS-DSP](https://developer.arm.com/documentation/102052/0000)


# Experiments