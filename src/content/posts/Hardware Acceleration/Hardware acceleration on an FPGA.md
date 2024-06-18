---
title: Hardware Acceleration on an FPGA
published: 2024-06-17
tags:
  - FPGA
  - AI
category: Projects
draft: false
---
# Abstract
This is a post to document our project on an FPGA board. We are going to use an FPGA board to accelerate the training of a KNN ML model.<br>
# Progress
1. [ ] Research
	- [ ] KRIA KR260 Robotics Starter Kit
	- [ ] hls4ml python package
	- [ ] QKeras (supported by hls4ml)
	- [ ] Under the working of KNNs
	- [ ] Parts for optimization in a KNN model
2. [ ] Coding
3. [ ] Testing
4. [ ] Application
# Part 1
## SOM Specs
- Components
	- SOM 
	- Carrier card
	- Thermal solution
- Zynq™ UltraScale+™ MPSoC EV (XCK26)
- 4GB [non-ecc] DDR4
- I/O expansions
	- x4 Pmod 12-pin interface
	- x1 Raspberry Pi HAT header with 26 I/Os
- x4 USB 3.0/2.0 interfaces
## Current development flow
![[Development Flow.png]]
## Parts to optimize
- Distance calculation types
	- Euclidean
	- Manhattan
	- Chebyshev
	- Minowski
- Sorting wrt distance and picking 1st K points
- Voting
	- Standard - Equal scheme
	- Weighted scheme
# Links
### Part 1
- [KRIA SOM specs](https://www.hackster.io/512359/amd-pervasive-ai-developer-contest-robotics-ai-study-guide-ae74d6)
- [Zynq UltraScale+ MPSoC: Software Developers Guide](https://www.xilinx.com/support/documents/sw_manuals/xilinx2022_2/ug1137-zynq-ultrascale-mpsoc-swdev.pdf)
- [AMD fundamentals of FPGA acceleration](https://www.xilinx.com/publications/events/developer-forum/2018-frankfurt/fundamentals-of-fpga-based-acceleration.pdf)
- [Scope of FPGA acceleration](https://www.linkedin.com/pulse/unlocking-power-fpga-based-acceleration-aiml-dakshita-l-vwzmc/)
- [Application of CV on FPGA - CERN](https://zenseact.com/thinking-fast-and-getting-it-right-software-company-zenseact-and-cern-wrap-up-joint-research-project-around-the-acceleration-of-deep-learning-algorithms/)
- [Fundamentals of KNN](https://www.geeksforgeeks.org/k-nearest-neighbours/)
- [Under the hood for KNN models](https://medium.com/swlh/under-the-hood-of-k-nearest-neighbors-knn-and-popular-model-validation-techniques-84ab0964d563)
- [KNN on Keras](https://medium.com/@sorenlind/nearest-neighbors-with-keras-and-coreml-755e76fedf36)
- [Converting Keras to QNN](https://github.com/google/qkeras/issues/1)
- [Habana Gaudi Intel](https://habana.ai/blogs/explore-hardware-acceleration-for-deep-learning/)
### Part 2
- [Getting started setup](https://github.com/amd/Kria-RoboticsAI)