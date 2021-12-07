---
title: "Prior Work"
date: 2021-11-01T01:26:43-07:00
draft: false
comments: false
ShowReadingTime: true
searchHidden: true
weight: 4
---

<!-- TODO:
- Need to add details on BLE and Thread specification
 -->

# BLE 5.0

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

# Thread and OpenThread

### Summary
- Operates on top of 802.15.4 (which handles PHY and MAC). 
- Intended for IoT and home automation situations
- Thread at its core: ipv6 based peer-to-peer mesh network
- ipv6 means good performance and reliability
- Thread implements UDP, IP Routing and 6LoWPAN. 

- Self healing and self maintaining network
  - Readjust if you add devices or move them around

Ref: [electroniclinic](https://www.electroniclinic.com/thread-protocol-architecture-and-topology-fully-explained/)

## Thread Primer

![img1](/ecem202a_project/images/thread_stack.png#center)

[Cite the openthread website, 2 other papers, and nordic site]

### Exploration: 
- [nordic cli example](https://infocenter.nordicsemi.com/index.jsp?topic=%2Fsdk_tz_v4.1.0%2Fthread_cli_example.html)
- [github issue](https://github.com/openthread/openthread/issues/4036)

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


Slave (MTD):

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

MQTT-SN Example:

in raspberry pi: 

        $ sudo /usr/local/sbin/wpantund -o NCPSocketNme /dev/ttyACM0 -o WPANInterfaceName wpan0
        $ sudo wpanctl <command>
        $ sudo wpanctl status
        > if joined, leave
        $ sudo wpanctl leave
        $ sudo wpanctl join -n OpenThread-1262
        $ 

to connect ncp try: https://groups.google.com/g/openthread-users/c/GIg2i5WYF9A 


  From github [ot-thread](https://github.com/openthread/openthread/issues/4918):
  "Discovering the location of services is a common problem in an IP-based network"  

<!-- TODO:

- Focus on literature review of comparison of protocols
- And also past implementations of localization using RSSI

 -->
