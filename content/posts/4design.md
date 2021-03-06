---
title: "Design"
date: 2021-11-01T01:26:43-07:00
draft: false
comments: false
ShowReadingTime: true
searchHidden: true
weight: 5
---


# Contents

- Hardware Platforms
- Software Stack
- BLE Application
- OpenThread Application
- Localization Methods using RSS
- Experiments


# The Hardware Platform

### The SoC: Nordic nRF52840


- (2x) Arduino Nano Sense 33 BLE
  - Beacon 1 
- (2x) nRF52840 Dongle
  - Beacon 2 
  - Beacon 3 
- (1x) nRF52840 Development Kit
  - Central device (polls beacons)

![Hardware](/ecem202a_project/images/hardware.png)

# The Software Stack

### Embedded Software Development:
- Segger Embedded Studio
- nRF5 SDK & nRF5 SDK for Thread and Zigbee
- nRF Connect+Programmer for flashing code
- CMSIS Libraries for Arm Cortex M microcontrollers

### Utilities and Other tools:
- Python + Matplotlib
- nRF BLE Sniffer
- nRF 802.15.4 Sniffer
- WireShark

# BLE Application

Main idea:
Beacons will use advertising channels.
Central device will filter out the advertisements via mac address periodically. Will fit them into buffers, and perform trilateration to get location information.

Projects:
- `software/ble_app/ble_app_beacon_arduino`
- `software/ble_app/ble_app_beacon_dongle`
- `software/ble_app/ble_app_central_dk`

_Note: hex files ready to flash can be found in Output/Release/Exe/<project_name>.hex for each project_

The central device solution:
- MAC address filtering:
  - Set BLE advertising filters with `nrf_ble_scan_filter_set`
  - Enabled them with `nrf_ble_scan_filters_enable`
- Handling a filter match
  - Using switch case `NRF_BLE_SCAN_EVT_FILTER_MATCH`
  - Advertising report variable `p_adv` now holds contents of advertising match
    - Access MAC address via: `p_adv->peer_addr.addr`
    - Acess RSSI via: `p_adv->rssi`


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

The central device solution:
- Timer creation using the `app_timer` module
  - After initialization, a callback can be configured
-  Callback: 
   -  Use the `otThreadGetNextNeighborInfo` function to get the next neighbor
   -  Then we can use the `my_neighbor_info` to access the neighbor info data structure
      -  RLOC (ID): `my_neighbor_info.mRloc16`
      -  Age (time since last update to neighbor info): `my_neighbor_info.mAge`
      -  Last RSSI: `my_neighbor_info.mLastRssi`

references:
- [ublox mqtt-sn beginner guide](https://www.u-blox.com/en/blogs/insights/mqtt-beginners-guide)
- [steve's internet guide mqttsn](http://www.steves-internet-guide.com/mqtt-sn/)


# Localization Methods using RSS
## Initial Model: Geometrical Application

Trilateration is a navigation position methodology based on simultaneous ranging from, traditionally, three trackers.Through the use of three beacons and their associated Received Signal Strength Indicator, RSS. Trilateration can be used to estimate the location of an unknown point in space. Distances (d_one, d_two, d_three) are measured by an RSS signal. The location of an unknown point of interest can be found by solving a system of quadratic equations. A baseline approach for Trilateration in python was used to build the intuiton and direction of this localization project. The motivating paper for this exploration is listed below and highly recommended for anyone interested in learning about this technique and overall discipline.




## Model Improvement using Fingerprinting Method: 


There are disadvantages of trilateration, however. Namely in the number of beacons required for precise accuracy, positioning with respect to the target, and susceptibility to noise. To address these concerns, inference methods were explored to leverage the advantafes of these methods - which can be calibrated to be more robust in real applications.Bayes theorem allows us to compute the most likely class for some measures RSS.
Reference: R. Faragher and R. Harle, "Location Fingerprinting With Bluetooth Low Energy Beacons," in IEEE Journal on Selected Areas in Communications, vol. 33, no. 11, pp. 2418-2428, Nov. 2015, doi: 10.1109/JSAC.2015.2430281.


### Deploying the updated model: CMSIS Libraries
[How to implement Bayesian with CMSIS-DSP](
https://developer.arm.com/documentation/102052/0000/Train-your-Bayesian-estimator-with-scikit-learn)
[How to implement Bayesian with SVM-DSP] https://developer.arm.com/documentation/102052/0000/Implement-your-SVM-with-CMSIS-DSP

Cons:
  The limitations of CMSIS ML aglorithms are plentiful. Currently, there are only a few supported wrappers for the expansive set within SK-learn, and compromises had to be done with respect to accuracy and model size. 

# Experiments:
The Experimental setup:

![room](/ecem202a_project/images/room.png)


Data was collected at the UCLA campus in the Kerchoff lounge. RSS measurements were taken using BLE and OpenThread Applications at fixed distances of one meter, two meters, and three meters from the receiver for three channels. This data is is in the "Data" folder of the github.



![rssi](/ecem202a_project/images/rssi.png)



Above is an image demonstrating the RSS values attained in the environment above, but at intervals of 0.5 meters from the origin up to three meters away.
There are additional images of data measurements in the github as well.
