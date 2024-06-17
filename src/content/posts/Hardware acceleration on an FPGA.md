---
title: Hardware Acceleration on an FPGA
published: 2024-06-17
tags: 
  - FPGA
  - KNN
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
- [KRIA SOM specs](https://www.hackster.io/512359/amd-pervasive-ai-developer-contest-robotics-ai-study-guide-ae74d6)
- [AMD fundamentals of FPGA acceleration](https://www.xilinx.com/publications/events/developer-forum/2018-frankfurt/fundamentals-of-fpga-based-acceleration.pdf)
- [Scope of FPGA acceleration](https://www.linkedin.com/pulse/unlocking-power-fpga-based-acceleration-aiml-dakshita-l-vwzmc/)
- [Fundamentals of knn](https://www.geeksforgeeks.org/k-nearest-neighbours/)
- [Under the hood for KNN models](https://medium.com/swlh/under-the-hood-of-k-nearest-neighbors-knn-and-popular-model-validation-techniques-84ab0964d563)
- [KNN on keras](https://medium.com/@sorenlind/nearest-neighbors-with-keras-and-coreml-755e76fedf36)
- [Converting keras to QNN](https://github.com/google/qkeras/issues/1)