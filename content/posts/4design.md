---
title: "Design"
date: 2021-11-01T01:26:43-07:00
draft: false
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

### BLE Primer

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

### Thread Primer

![img1](/ecem202a_project/images/thread_stack.png#center)

[Cite the openthread website, 2 other papers, and nordic site]

- Operates on top of 802.15.4 (which handles PHY and MAC). 
- Intended for IoT and home automation situations
- Thread at its core: ipv6 based peer-to-peer mesh network
- ipv6 means good performance and reliability
- Thread implements UDP, IP Routing and 6LoWPAN. 

- Self healing and self maintaining network
  - Readjust if you add devices or move them around

Ref: [electroniclinic](https://www.electroniclinic.com/thread-protocol-architecture-and-topology-fully-explained/)

## Network Design

All will be full thread devices - to avoid sleep.

[info on node types](https://openthread.io/guides/thread-primer/node-roles-and-types)

- Border Router: raspberry pi + ncp dongle
  - connects thread network to PC
- End devices - Beacons (2 dongles+1 arduino) - are children
- Lead device - arduino
  - uses coAP
  - controls requests for REEDs to become routers

### Attempt 1: communicate RSSI based on hardware layer functions.

### Attempt 2: UDP packets

### Attempt 3: use mqtt-sn 
- Lightweight version of MQTT, using UDP
- Friendly for sensor networks (sleep mode, low energy, limited bandwidths)
- Requires a connection to a broker before being able to send/receive msgs
- Uses subscription based communication
- Publishes to a topic, other nodes can subscribe to the topic and receive the messages

references:
- [ublox mqtt-sn beginner guide](https://www.u-blox.com/en/blogs/insights/mqtt-beginners-guide)
- [steve's internet guide mqttsn](http://www.steves-internet-guide.com/mqtt-sn/)

### RSSI in Thread/802.15.4

Few functions/data structures to keep in mind:
- [otNeighborInfo Struct Reference](https://infocenter.nordicsemi.com/index.jsp?topic=%2Fsdk_tz_v4.0.0%2Fstructot_neighbor_info.html&resultof=%22%72%73%73%69%22%20)
- [otChildInfo Struct Reference](https://infocenter.nordicsemi.com/index.jsp?topic=%2Fsdk_tz_v4.0.0%2Fstructot_child_info.html&resultof=%22%72%73%73%69%22%20)
- [otThreadParentResponseInfo Struct Reference](https://infocenter.nordicsemi.com/index.jsp?topic=%2Fsdk_tz_v4.0.0%2Fstructot_thread_parent_response_info.html&resultof=%22%72%73%73%69%22%20)

# Location from RSSI
## Initial Model: Geomtrical Solution

- Trilateration

## Improving the Model: SVM

### Deploying the updated model: CMSIS Libraries
[How to implement SVM with CMSIS-DSP](https://developer.arm.com/documentation/102052/0000)


# Experiments