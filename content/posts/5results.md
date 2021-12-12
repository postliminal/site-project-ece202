---
title: "Results"
date: 2021-11-01T01:26:43-07:00
draft: false
comments: false
ShowReadingTime: true
searchHidden: true
weight: 6
---
# 1. Noisy measurements of RSSI in BLE and 802.15.4

- python plots
  - if possible have multiple adv channels
  - and compare aggregate/default/average
- explanation
- could do some signal analysis (variance, etc?)

# 2. Localization results (BLE vs. Thread)

It should be noted that OpenThread is a self-healing network, and since "Self-healing allows a routing-based network to operate when a node breaks down or when a connection becomes unreliable. [1]" The synchonicity of this network differs significantly from BLE. The BLE implemented does not have this feature for all nodes, and this is highly visible in the data collected when comparing results. BLE is a continous spectrum of data, whilst OpenThread is not. The topology of OpenThread changes as a function of time. This is an advantage from a reliability perspective, but ultimately created an inequivalent comparison. The metric for comparison therefore BLE and OpenThread ultimately became founded on raw RSSI values. The RSSI values for BLE and OpenThread offered no significant performance in the environment tested. BLE does have greater performance in terms of latency, but this is once again due to OpenThread's self-healing feature.

With regards to the RSSI values obtained using both BLE and OpenThread. OpenThread was much more consistent in the values reported. The RRSI values reported in the data are pretty consistent and do decreases as the distance increases from the receiver. An interesting observation is that the RSSI values are clustered to a smaller range of values, such that there is not much variance in the RSSI values. This is somewhat expected since, as noted, the topology is "self-healing".

There is a larger continous spectrum in the BLE values obtained in the experiments which speaks to the high variance and faultiness of a BLE network.

These phenomenon is noted in the "RSSI Inspection" notebook in the github for this project.


- 


[1] - Wikipedia contributors. "Mesh networking." Wikipedia, The Free Encyclopedia. Wikipedia, The Free Encyclopedia, 9 Dec. 2021. Web. 12 Dec. 2021.
