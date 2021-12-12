---
title: "Results"
date: 2021-11-01T01:26:43-07:00
draft: false
comments: false
ShowReadingTime: true
searchHidden: true
weight: 6
---
# 1. Noisy measurements of RSS in BLE and 802.15.4

![im1](/ecem202a_project/images/1m_rssi_data_ch3X_1.png)


![im2](/ecem202a_project/images/2m_rssi_data_ch3X_1.png)

The above two images show the RSS collected. As expected the RSS degrades as the distance between the beacons and the receiver increases.

The below image shows a snapshot of the ML model's ability to predict the distance from a RSS-fingerprint map to estimate the location of an object. 

![im3](/ecem202a_project/images/ML_plotpdf.pdf)







# 2. Localization results (BLE vs. Thread)

It should be noted that OpenThread is a self-healing network, and since "Self-healing allows a routing-based network to operate when a node breaks down or when a connection becomes unreliable. [1]" The synchonicity of this network differs significantly from BLE. The BLE implemented does not have this feature for all nodes, and this is highly visible in the data collected when comparing results. BLE is a continous spectrum of data, whilst OpenThread is not. The topology of OpenThread changes as a function of time. This is an advantage from a reliability perspective, but ultimately created an inequivalent comparison. The metric for comparison therefore BLE and OpenThread ultimately became founded on raw RSS values. The RSS values for BLE and OpenThread offered no significant performance in the environment tested. BLE does have greater performance in terms of latency, but this is once again due to OpenThread's self-healing feature.

With regards to the RSS values obtained using both BLE and OpenThread. OpenThread was much more consistent in the values reported. The RRSI values reported in the data are pretty consistent and do decreases as the distance increases from the receiver. An interesting observation is that the RSS values are clustered to a smaller range of values, such that there is not much variance in the RSS values. This is somewhat expected since, as noted, the topology is "self-healing".

There is a larger continous spectrum in the BLE values obtained in the experiments which speaks to the high variance and faultiness of a BLE network.

These phenomenon is noted in the "RSS Inspection" notebook in the github for this project.


Whilst the group was able to implement a machine learning model developed in Segger with CMSIS' DSP toolbox, further work would be needed to validate the results more accurately. As of now, the values for the BLE configuration fit the distance measurements magnitude expected. Please see the "Future Work" section for elaboration.

** All scripts used to generat the work here is in the "Data" folder of the asscociated repo

[1] - Wikipedia contributors. "Mesh networking." Wikipedia, The Free Encyclopedia. Wikipedia, The Free Encyclopedia, 9 Dec. 2021. Web. 12 Dec. 2021.
