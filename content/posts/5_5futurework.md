---
title: "Future Work"
date: 2021-12-10T03:02:21-08:00
draft: false
comments: false
ShowReadingTime: true
searchHidden: true
weight: 7
---

Future Experimental Work to Consider:
- As mentioned in the results section, the group was able to re-configure a machine learning framework, test it using open - sourced data, and implement on a Nordic device using Segger. The results magnitude aligns with what was expected, but had a sign reversal that needs to be further elaborated. The discerepancy is believed to be due to a configuration issue, and not a fundamental understanding of the implementation since CMSIS' instructions were followed which also utilizes SK-learn.

However, the SDK that operates the OpenThread application was not able to run the ML pipeline that was compiled on Segger successfully. Further work is needed in this implementation. 



Aspects that were worked on include:
- Running initial tinyML wake-word models within Segger in an attempt to streamline environment dependencies due to existing environment support/capabilities 
- Deploying developed ML models outside of those supported by the CMSIS DSP toolbox 
- Limitations of hardware space highly impacted the models and condigurations we were able to deploy due to size and storage
- Overall, whilst the intersections of embedded systems and its capabilities to run Machine Learning models is highly evolving. The groups goal of employing models within fundamental embeeded system building blocks was challenging in the integration of sub-units. For example, CMSIS' DSP features are still developing and so are its capabilities to deploy standard ML frameworks used in SK-learn
- Tensorflow's TinyML library is a great resource that could also not be supported outside of the Arduino environment since many other approaches could not support it



