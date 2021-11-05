---
title: "Proposal"
date: 2021-11-01T01:26:06-07:00
draft: false
comments: false
ShowReadingTime: true
searchHidden: true
weight: 1
---

# Project Proposal

## 1. Motivation & Objective

Indoors localization has been a highly researched topic for decades. Since GPS signals can’t reach devices inside buildings, alternative methods using radio signals (Bluetooth, 802.15.4, wifi), audio signals, visual signals, etc. have been devised and published. Given that these sensing technologies (radio, audio, video, depth) continue to improve, the indoors localization problem is still relevant and continues to be actively researched. Therefore, we seek to contribute to the ongoing research by approaching the localization problem via the implementation and experimentation of some of these algorithms in a resource constrained computing environment (Arduino Nano Sense 33 BLE). We will focus on the localization problem using two types of radio communication: Bluetooth Low Energy (BLE) and Thread (using OpenThread). 
In order to provide a more realistic testing scenario, we will include other background processes such as keyword recognition via the onboard microphone and visual feedback via an LCD display. Since the localization tasks require very precise timing and synchronization, this setup will let us experiment and characterize the performance of different scheduling schemes as well as find tradeoffs in accuracy and performance. The goal is to familiarize ourselves with some of the new capabilities on the board, whilst creating a benchmark for the effectiveness, capabilities, and overall limitations of the board in this task that utilize communication systems, sensors, and TinyML. 


## 2. State of the Art & Its Limitations

As more tasks are demanded from IoT devices, having multiple processes on a system with varying priorities becomes common. Yet there exists room to further characterize the scheduling of applications using radio for localization applications. As discussed in the objective above, there exist many obstacles in current applications of localization applications. The direction of localization greatly benefits from the features of the Arduino Nano Sense 33 BLE through the ubiquitousness of BLE and Thread protocols in low power form factors. Therefore, the ability to successfully orchestrate our objective showcases the growth of embedded systems tackling localization applications in ways that traditional methods have not. Currently, most localizations are contingent on WiFi methods that have varying accuracy and require high power sources. 


## 3. Novelty & Rationale

Our approach will use the Arduino’s BLE and Openthread processes in a more realistic scenario, by evaluating the performance of a higher priority process (wake-word recognition) as a localization process is running. The motivation of the implementation is to delve deeper into the inner workings of these operations and assess the tradeoffs of each configuration. The chances of success are high since the board supports Bluetooth 5.1 which has new localization features. Furthermore, increased research and development of the OpenThread project will allow us to work more efficiently when using this protocol. We plan to take advantage of existing frameworks such as nrfConnect, BLEscanner, etc. Our decision to characterize and evaluate parameters (e.g sampling rate, scheduling schemes, filtering schemes, tinyml model architecture) will further allow us to distinguish optimal cases and limitations of the Arduino Nano Sene 33 BLE.

## 4. Potential Impact

Real time localization systems (RTLS) are increasing in importance as more automated/autonomous machines and robots are deployed in workplace environments, where people and robots have to work together. Therefore, our project’s success will help clarify the limitations and advantages of the Arduino Nano 33 BLE Sense’s hardware in realistic localization uses. 
We will be able to optimize performance for time critical processes/tasks where latency and performance are essential by creating a deterministic approach to scheduling. The results will highlight best practices when using the Arduino Nano 33 Ble Sense and similar embedded systems. 


## 5. Challenges

A challenge of the project will be successfully orchestrating multiple subprocesses effectively and maximizing the performance within each. Some of these subprocesses include the inference of machine learning models, signal processing of BLE and thread signals, and performing the localization algorithm. A notable risk is the serial process of events that cascades into each submodule. There is a great benefit to maximizing each component within the project for a comparison of the results using different processes. Hence the success of the overall project is greatly impacted by any bottlenecks or inefficiencies. Additional risks include the lack of familiarity with aspects of the project. Much of the frameworks that are planned to be used such are uncharted domains and will require significant understanding in order to accomplish the objective as desired. Additional possible challenges are the scheduling and synchronization between arduinos.

## 6. Requirements for Success

- Writing/editing drivers based on documentation
- Ability to implement findings from research papers
- Rapid iterations and realization of minimum viable products
- Using Bluetooth 5.1 and OpenThread to the fullest
- Course material, office hours, CampusWire


## 7. Metrics of Success

Metrics for success at the system and subunit levels are optimizing parameters in the pipeline to attain favorable RSSI, RMSE, and the evaluation of latency and performance. Parameters within the architecture of the implementation include the size of the program, task deadlines met, and accuracy of the algorithms developed/implemented. 


## 8. Execution Plan

Key tasks in the project can be assessed as the process of developing a Machine Learning Pipeline for a spoken word, implementation of the localization process, and implementation of the BLE and Openthread processes. Within these processes, a goal is to effectively optimize processing and parameters respectively. The team is partitioning tasks according to priority and familiarity with concepts.

Side tasks Include:
Wake-word recognition
LCD screen
System configuration/setup
Firmware and Client data processing software
Data collection
Audio
BLE
Thread
Initial Results
Scheduling schemes
Execution of experiments
Evaluation of results and presentation (what worked and what didnt)


## 9. Related Work

### 9.a. Papers

below).
- Good overview on the indoors localization field (2017) https://www.ncbi.nlm.nih.gov/pmc/articles/PMC5580254/ 
- Performance evaluation of ble localization work (2014) https://onlinelibrary.wiley.com/doi/10.1002/ett.2864
- Existing implementation of ble loc on arduino nano sense (2021) https://www.ncbi.nlm.nih.gov/pmc/articles/PMC8347277/ 
- Location fingerprinting with BLE beacons (2015):
- Location Fingerprinting With Bluetooth Low Energy Beacons.pdf 
- SurroundSense: mobile phone localization via ambience fingerprinting - https://dl.acm.org/doi/abs/10.1145/1614320.1614350


### 9.b. Datasets

"Warden P. Speech Commands: A public dataset for single-word speech recognition, 2017. Available from: http://download.tensorflow.org/data/speech_commands_v0.01.tar.gz".

### 9.c. Software

- Arduino libs for prototyping
- Nordic SDK/softdevices
- nRF Connect for Desktop
- Python nRF sniffer (802.15.4/BLE)
- TinyML
- Openthread
- Mbed OS
- Zephyr OS
- https://www.openbeacon.org/about.html 


## 10. References

A Review of Pedestrian Indoor Positioning Systems for Mass Market Applications - 
Correa, Alejandro et al. “A Review of Pedestrian Indoor Positioning Systems for Mass Market Applications.” Sensors (Basel, Switzerland) vol. 17,8 1927. 22 Aug. 2017, doi:10.3390/s17081927

Performance evaluation of bluetooth low energy in indoor positioning systems- Contreras, David, Castro, Mario, and de la Torre, David Sánchez (2017), Performance evaluation of bluetooth low energy in indoor positioning systems, Trans. Emerging Tel. Tech., 28: e2864. doi: 10.1002/ett.2864

A Practice of BLE RSSI Measurement for Indoor Positioning - Ramirez, Ramiro et al. “A Practice of BLE RSSI Measurement for Indoor Positioning.” Sensors (Basel, Switzerland) vol. 21,15 5181. 30 Jul. 2021, doi:10.3390/s21155181

SurroundSense: mobile phone localization via ambience fingerprinting - Martin Azizyan, Ionut Constandache, and Romit Roy Choudhury. 2009. SurroundSense: mobile phone localization via ambience fingerprinting. In Proceedings of the 15th annual international conference on Mobile computing and networking(MobiCom '09). Association for Computing Machinery, New York, NY, USA, 261–272. DOI:https://doi.org/10.1145/1614320.1614350

<br/> - Arduino/TinyML: https://www.arduino.cc 
<br/> - nRF Connect for Desktop: https://www.nordicsemi.com/Products/Development-tools/nrf-connect-for-desktop
<br/>Python nRF sniffer (802.15.4/BLE): https://github.com/NordicSemiconductor/nRF-Sniffer-for-802.15.4
<br/>Openthread: https://openthread.io
<br/>Mbed OS: https://os.mbed.com/mbed-os/
<br/>Zephyr OS:https://www.zephyrproject.org
<br/>OpenBeacon : https://www.openbeacon.org/about.html 
<br/>Nordic SDK/softdevices: https://infocenter.nordicsemi.com/index.jsp?topic=%2Fug_gsg_ses%2FUG%2Fgsg%2Fsoftdevices.html

