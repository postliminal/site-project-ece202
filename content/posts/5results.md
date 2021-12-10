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