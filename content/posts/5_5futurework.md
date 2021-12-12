---
title: "Future Work"
date: 2021-12-10T03:02:21-08:00
draft: false
comments: false
ShowReadingTime: true
searchHidden: true
weight: 7
---

# Everything that we weren't able to do we can include it here nicely and explain what went wrong

- branches we didn't get to combine
  - multitask
  - wakework recog task

- any future config changes
  - the sweeps
  - or other sweeps

- any processing that could improve results


Aspects that were worked on include:
- Running initial tinyML wake-word models within Segger in an attempt to streamline environment dependencies due to existing environment support/capabilities 
- Deploying developed ML models outside of those supported by the CMSIS DSP toolbox 
- Limitations of hardware space highly impacted the models and condigurations we were able to deploy due to size and storage
- Overall, whilst the intersections of embedded systems and its capabilities to run Machine Learning models is highly evolving. The groups goal of employing models within fundamental embeeded system building blocks was challenging in the integration of sub-units. For example, CMSIS' DSP features are still developing and so are its capabilities to deploy standard ML frameworks used in SK-learn
- Tensorflow's TinyML library is a great resource that could also not be supported outside of the Arduino environment since many other approaches could not support it


# include timeline? list of tasks?

# automation of parameters 
- could be directly applied to neural architecture search of future models that use peripherals?
- would have to find/surface obsucre configs and macros
  - then automate script that replaces text, calls gcc compiles, then launches data collection w/ hardware in the loop.

