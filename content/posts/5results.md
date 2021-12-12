---
title: "Results"
date: 2021-11-01T01:26:43-07:00
draft: false
comments: false
ShowReadingTime: true
searchHidden: true
weight: 6
---

_we only need to do a few sweeps and we get something solid_

**take photos!!!**

# 1. Noisy measurements of RSSI in BLE and 802.15.4

- python plots
  - if possible have multiple adv channels
  - and compare aggregate/default/average
- explanation
- could do some signal analysis (variance, etc?)

# 2. Localization results (BLE vs. Thread)

It should be noted that OpenThread is a self-healing network, and since "Self-healing allows a routing-based network to operate when a node breaks down or when a connection becomes unreliable. [1]" The synchonicity of this network differs significantly from BLE. The BLE implemented does not have this feature, and this is highly visible in the data collected when comparing results. BLE is a continous spectrum of data, whilst OpenThread is not. The topology of OpenThread changes as a function of time. This is an advantage from a reliability perspective, but ultimately created an inequivalent comparison. The metric for comparison therefore BLE and OpenThread ultimately became founded on raw RSSI values.





Throughout the data collection of the RSSI using OpenThread and BLE,  



Current narrative:
- thread is not meant for this application
  - self healing/automated network changes structure
  - give example of applications meant for thread

- unable to disable exponential backoff when using `otGetNeighborinfo` without having to recompile the libraries manually
  - potentially removing that thread certification?? idk - should cite a source if we wish to say this

- 

# 3. A sweep of bluetooth configs
- easiest could be window changes 
  - median x choice of N
  - mean + choice of N


[1] - Wikipedia contributors. "Mesh networking." Wikipedia, The Free Encyclopedia. Wikipedia, The Free Encyclopedia, 9 Dec. 2021. Web. 12 Dec. 2021.
