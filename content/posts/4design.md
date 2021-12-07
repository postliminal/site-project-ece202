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

Main idea:
Beacons will use advertising channels.
Central device will filter out the advertisements via mac address periodically. Will fit them in circular buffers (window sizes).



# Thread Application



Options:
- central device has to be parent
- beacons have to be child
- Still need to know where devices are...
- poll by asking child info and parsing
connected to children. 

Now... how do we ensure automatic connection?
Todo: 
- [mqtt sn example](https://infocenter.nordicsemi.com/index.jsp?topic=%2Fsdk_tz_v3.1.0%2Fthread_mqttsn_example.html)
- [border router example](https://infocenter.nordicsemi.com/index.jsp?topic=%2Fcom.nordic.infocenter.thread_zigbee.v3.0.0%2Fthread_border_router.html)
- [802 sniffer](https://infocenter.nordicsemi.com/index.jsp?topic=%2Fug_sniffer_802154%2FUG%2Fsniffer_802154%2Fintro_802154.html)

If all else fails, use border router to define macro variables as a arguments in a function call.


## Network Design

All will be full thread devices - to avoid sleep.

[info on node types](https://openthread.io/guides/thread-primer/node-roles-and-types)

Leader is chosen automatically.
Can only choose if device is:
- Full thread device
  - Router
  - Router eligible device (REED) - can become a router
  - Full end device
- Minimal thread device

Our proposed network:
- Border Router: raspberry pi + ncp dongle
- End devices - Beacons (2 dongles+1 arduino) - children
- Router(?) - arduino
  - to request infor from children




Request info using: Mesh-Local EID



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
## Initial Model: Geometrical Application

Trilateration is a navigation position methodology based on simultaneous ranging from, traditionally, three trackers.Through the use of three beacons and their associated Received Signal Strength Indicator, RSSI. Trilateration can be used to estimate the location of an unknown point in space. Distances (d_one, d_two, d_three) are measured by an RSSI signal. The location of an unknown point of interest can be found by solving a system of quadratic equations. A baseline approach for Trilateration in python was used to build the intuiton and direction of this localization project. The motivating paper for this exploration is listed below and highly recommended for anyone interested in learning about this technique and overall discipline.


R. Faragher and R. Harle, "Location Fingerprinting With Bluetooth Low Energy Beacons," in IEEE Journal on Selected Areas in Communications, vol. 33, no. 11, pp. 2418-2428, Nov. 2015, doi: 10.1109/JSAC.2015.2430281.



## Model Improvements: 

There are disadvantages of trilateration, however. Namely in the number of beacons required for precise accuracy, positioning with respect to the target, and susceptibility to noise. To address these concerns, inference methods were explored to leverage the advantafes of these methods - which can be calibrated to be more robust in real applications.Bayes theorem allows us to compute the most likely class for some measures RSSI.



### Deploying the updated model: CMSIS Libraries
[How to implement Bayesian with CMSIS-DSP]
https://developer.arm.com/documentation/102052/0000/Train-your-Bayesian-estimator-with-scikit-learn


# Experiments
