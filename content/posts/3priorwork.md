---
title: "Prior Work"
date: 2021-12-01T01:26:43-07:00
draft: false
comments: false
ShowReadingTime: true
searchHidden: true
weight: 4
---

# Bluetooth - BLE 5.0

A wireless communication protocol that is (almost if not already) ubiquitous. Released in 2016, BLE 5.0 introduced a few changes that make bluetooth technology suitable for more applications. New features allow:
- larger bandwidth transmissions (higher throughput = higher data speeds)
- multi device connection (e.g. now you can send music to two pairs of headphones from one device)
- larger advertising packets allow better pairing + other applications (**beacons**!). 

We will take advantage of larger advertising packets for the localization application. 

### BLE Primer

[Bluetooth 5.0 Specification](https://www.bluetooth.org/docman/handlers/downloaddoc.ashx?doc_id=457080)

The Bluetooth specification provides a full stack solution for communication. Therefore, we don't need anything else to create the solution.

![ble advertising](/ecem202a_project/images/ble_adv_channels.png)
BLE advertising channels + overlay with wifi channels showing less likelihood for interference in these channels.
Source: DOI 10.1109/JSAC.2015.2430281

### Advertising

By default occurs over channels 37, 38 and 39, which are spread out over the 2.4MHz band, and are precisely located at the edges of the wifi band to help reduce wifi interference. 

With the nordic SDK, advertisements can be precisely configured with various settings. We'll explore the use of the following:
- Window size
- RSSI dB filtering
- Advertising interval

### RSSI

Received Signal Strength Indicator. This value measures the received signal strength in dB and can be used to esitmate the distance of the receiver from the transmitter device. 

The RSSI is represented using a byte inside of the manufacturer specific data. 

# Thread and OpenThread

### Summary
- Operates on top of 802.15.4 - 2.4 GHz radio band (which handles PHY and MAC). 
- Intended for IoT and home automation situations
- Thread at its core: ipv6 based peer-to-peer mesh network
  - ipv6 means good performance and reliability
- Thread implements UDP, IP Routing and 6LoWPAN. 
- Self healing and self maintaining network
  - Readjust if you add devices or move them around

![Thread stack](/ecem202a_project/images/thread_stack.png)



### References: 

- [openthread site](https://openthread.io/)
- [nordic thread sdk](https://infocenter.nordicsemi.com/index.jsp?topic=%2Fstruct_sdk%2Fstruct%2Fsdk_thread_zigbee_latest.html)
- [electroniclinic](https://www.electroniclinic.com/thread-protocol-architecture-and-topology-fully-explained/)

### Exploration: 
- [nordic cli example](https://infocenter.nordicsemi.com/index.jsp?topic=%2Fsdk_tz_v4.1.0%2Fthread_cli_example.html)

Leader (FTD):

        > reset
        >
        > dataset init new
        Done
        > dataset commit active
        Done
        > dataset active
        Active Timestamp: 1
        Channel: 15
        Channel Mask: 07fff800
        Ext PAN ID: ab6f0f99db116ec3
        Mesh Local Prefix: fd19:ea13:f1fa:e501/64
        Master Key: 1222558b01070cb6211ae2ad888f9429
        Network Name: OpenThread-096e
        PAN ID: 0x096e
        PSKc: c2d539fc2f64b8b56713de1de2f6de8f
        Security Policy: 0, onrcb
        Done
        > ifconfig up
        Done
        > thread start
        Done
        > state
        detached
        Done
        > state
        detached
        Done
        > state
        leader
        Done
        > neighbor table


Child (MTD):

        > reset
        > 
        > dataset clear
        Done
        > dataset masterkey 1222558b01070cb6211ae2ad888f9429
        Done
        > dataset commit active
        Done
        > dataset active
        Master Key: 1222558b01070cb6211ae2ad888f9429
        Done
        > ifconfig up
        Done
        > thread start
        Done
        > state
        detached
        Done
        > state
        detached
        Done
        > state
        detached
        Done
        > state
        detached
        Done
        > state
        child
        Done
        

CLI commands:

        > child 1
        Child ID: 1
        Rloc: 5401
        Ext Addr: 53e8f050a7d4a7dd
        Mode: rsdn
        Net Data: 183
        Timeout: 240
        Age: 220
        Link Quality In: 3
        RSSI: -18
        Done
        > rloc16
        1000 (if router)
        1001 (if child)

in raspberry pi: 

        $ sudo wpanctl status
        > get status
        >> ** navigate to your raspberry pi IP address **
        >> ** Join > Select your network > use masterkey to join network **

Now we have a working network with 1 leader, one border router (gateway to the internet), and one child


# Setting up the development environment

## Segger Embedded Studio

Huge thanks to: [this element14 tutorial](https://community.element14.com/products/roadtest/b/blog/posts/tutorial-02-part-1-developing-nrf52840-application-arduino-nano-33-ble-sense-roadtest)

- Find example in SDK as a template
- Copy (into an empty dir for your new project) the following:
  - `main.c`
  - `pca10056/blank/ses/flash_placement.xml`
  - `pca10056/blank/ses/<projectname>.emProject`
  - `pca10056/blank/config/sdk_config.h`
- Open the .emproject file and make the following edits:
  - Replace `../../../../../..` with your `/<path_to_sdk_root_dir>`
  - Remove `../../../config;` from `c_user_include_directories`
  -  Remove `../../..;` from `c_user_include_directories` value
  -  Replace `../config;` to `.;`
  -  Replace `../../../main.c` to `main.c`
  -  Replace `../config/sdk_config.h` to `sdk_config.h`


# Quick addition to SDK to use NRF with arduino

Big thanks to: [this repo](https://github.com/drewvigne/arduino_nano_33_ant)

In order to use NRF high level API functions, we need to map peripherals, pins, ports on the arduino board to the NRF functions/macros/etc.
The SDK uses `<sdk_path>/components/boards/boards.h` to conditionally include the corresponding header file for the hardware of our choice (selection done in project settings via preprocessor flag).

Steps:
 - edit `boards.h` by adding the following line (right before `#elif defined(CUSTOM_BOARD_INC)`)
      
        #elif defined(ARDUINO_BLE_33)
          #include "arduino_ble_33.h"
- Copy the file in `components/boards/arduino_ble_33.h` to `<sdk_path>/components/boards/boards.h`
- Modify project file's preprocessor flag to `ARDUINO_BLE_33`


<!-- TODO:

- Focus on literature review of comparison of protocols
- And also past implementations of localization using RSSI

 -->
