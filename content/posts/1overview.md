---
title: "Overview"
date: 2021-12-02T01:26:06-07:00
draft: true
comments: false
ShowReadingTime: true
searchHidden: true
weight: 2
# cover:
#   image: /ece202-fall21-project/images/Tux.png
---

<!-- <base href="{{ .Site.BaseURL }}"> -->

# 1. Overview

## Problem:

With the rise and continuous update of various IoT communication standards it is hard to keep track of what is the most suitable option. Two standards, Bluetooth (BLE 5.0 standard) and Thread (implemented using OpenThread), are either massively adopted (BLE) or rapidly gaining popularity (thread). However, there has not been a recent analysis between these two protocols.

## Project Goals:

Make an updated analysis between these two protocols. By using various radio configurations for both protocols we can get a better understanding on their performance and limitations.

## Project Objectives and Scopes:

Doing a full analysis on both protocols would require a lot more time than what we have: six weeks. Therefore, we're reducing the scope to evaluating both protocols in a localization application scenario. We'll evaluate system accuracy, latency and overall protocol ease of use.

## Key Deliverables:

### Software:
- BLE application files
  - Beacon
  - Central
- Thread application files
  - Beacon
  - Central

### Documentation:
- Public website containing:
  - Instructions to recreate system
  - Analysis and evaluation of findings
- Open access github repository

## Proposed Schedule:

Fall Quarter 2021:
- **Week 4:** Define group members and decide project idea
- **Week 5:** Literature review and research of relevant work
- **Week 6:** Write project proposal
- **Week 7:** Setup software development environments and start getting acquainted with Nordic nRF SDK
- **Week 8:** Use hardware vendor documentaiton to develop custom solution to collect measurements and communicate it to PC
- **Week 9:** Conclude data collection and proceed to analysis
- **Week 10:** Evaluate work, write conclusions and review code

## Potential Limitations and Setbacks:

- Software incompatibility between libraries
- Compilation problems
- Noise in radio data
<!-- 
### how to insert code blocks

    indents = 4;
    return null;

### images:

![img1](/ece202-fall21-project/images/Tux.png#center) -->
