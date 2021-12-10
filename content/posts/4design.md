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
  - Beacon 1 MAC: 
  <!-- - Central MAC: D4:6B:03:E9:AD:E7 -->
- (2x) nRF52840 Dongle
  - Beacon 2 MAC: 
  - Beacon 3 MAC: 
- (1x) nRF52840 Development Kit
  - Central device (polls beacons)

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
Central device will filter out the advertisements via mac address periodically. Will fit them into buffers, and perform trilateration to get location information.

### TODO: fix filenames of projects/hex files

Projects:
- `software/ble_app/ble_app_beacon_arduino`
- `software/ble_app/ble_app_beacon_dongle`
- `software/ble_app/ble_app_beacon_dk`
- `software/ble_app/ble_app_central_dk`

_Note: hex files ready to flash can be found in Output/Release/Exe/<project_name>.hex for each project_


## *************** TODO: explain code ^^ !


# Thread Application
### Proposed network:
- 2 MTD (minimal thread devices) 
  - CLI USB example for dongle
  - CLI USB example for arduino
  - _children/end devices_
- 1 NCP (network co-processor) + Raspberry pi
  - NCP example for dongle
  - _router+gateway_
- 1 FTD (full thread device)
  - thread_cli_uart example for development kit
  - _leader_

With this network we can make the FTD the leader (capable of easily polling children devices and neighboring routers).

_Note: automatic network creation, commissioning and joining are beyond the scope of this project, which is why the CLI's / web GUI will be used._

- [border router example](https://infocenter.nordicsemi.com/index.jsp?topic=%2Fcom.nordic.infocenter.thread_zigbee.v3.0.0%2Fthread_border_router.html)

Possibility to ping all (multicast) via:

      > ping ff02::1

Projects:
- `software/openthread_app/openthread_cli_arduino`
  - based on cli/mtd/usb/ example
- **MISSING** `software/openthread_app/openthread_cli_dongle`
  - based on cli/mtd/usb/ example
- `software/openthread_app/openthread_cli_dk`
  - based on cli/ftd/uart example
- `software/openthread_app/openthread_ncp_dongle`
  - based on ncp example

_Note: hex files ready to flash can be found in Output/Release/Exe/<project_name>.hex for each project_

## *************** TODO: explain code ^^ !

references:
- [ublox mqtt-sn beginner guide](https://www.u-blox.com/en/blogs/insights/mqtt-beginners-guide)
- [steve's internet guide mqttsn](http://www.steves-internet-guide.com/mqtt-sn/)

### RSSI in Thread/802.15.4

Few functions/data structures to keep in mind:
- [otNeighborInfo Struct Reference](https://infocenter.nordicsemi.com/index.jsp?topic=%2Fsdk_tz_v4.0.0%2Fstructot_neighbor_info.html&resultof=%22%72%73%73%69%22%20)


# Location from RSSI
## Initial Model: Geometrical Application

Trilateration is a navigation position methodology based on simultaneous ranging from, traditionally, three trackers.Through the use of three beacons and their associated Received Signal Strength Indicator, RSSI. Trilateration can be used to estimate the location of an unknown point in space. Distances (d_one, d_two, d_three) are measured by an RSSI signal. The location of an unknown point of interest can be found by solving a system of quadratic equations. A baseline approach for Trilateration in python was used to build the intuiton and direction of this localization project. The motivating paper for this exploration is listed below and highly recommended for anyone interested in learning about this technique and overall discipline.


R. Faragher and R. Harle, "Location Fingerprinting With Bluetooth Low Energy Beacons," in IEEE Journal on Selected Areas in Communications, vol. 33, no. 11, pp. 2418-2428, Nov. 2015, doi: 10.1109/JSAC.2015.2430281.



## Model Improvements: 

There are disadvantages of trilateration, however. Namely in the number of beacons required for precise accuracy, positioning with respect to the target, and susceptibility to noise. To address these concerns, inference methods were explored to leverage the advantafes of these methods - which can be calibrated to be more robust in real applications.Bayes theorem allows us to compute the most likely class for some measures RSSI.



### Deploying the updated model: CMSIS Libraries
[How to implement Bayesian with CMSIS-DSP](
https://developer.arm.com/documentation/102052/0000/Train-your-Bayesian-estimator-with-scikit-learn)

Cons:
  The limitations of CMSIS ML aglorithms are plentiful. Currently, there are only a few supported wrappers for the expansive set within SK-learn, and compromises had to be done with respect to accuracy and model size. 

# Experiments
