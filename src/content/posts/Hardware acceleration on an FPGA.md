---
title: Draft Example
published: 2024-06-17
tags: [FPGA, KNN, AI]
category: Examples
draft: false
---
- [KRIA Som specs](https://www.hackster.io/512359/amd-pervasive-ai-developer-contest-robotics-ai-study-guide-ae74d6)
- [AMD fundamentals of FPGA acceleration](https://www.xilinx.com/publications/events/developer-forum/2018-frankfurt/fundamentals-of-fpga-based-acceleration.pdf)
- [Scope of FPGA acceleration](https://www.linkedin.com/pulse/unlocking-power-fpga-based-acceleration-aiml-dakshita-l-vwzmc/)
- [Fundamentals of knn](https://www.geeksforgeeks.org/k-nearest-neighbours/)
- [Under the hood for KNN models](https://medium.com/swlh/under-the-hood-of-k-nearest-neighbors-knn-and-popular-model-validation-techniques-84ab0964d563)
- [KNN on keras](https://medium.com/@sorenlind/nearest-neighbors-with-keras-and-coreml-755e76fedf36)
- [Converting keras to QNN](https://github.com/google/qkeras/issues/1)

# Parts to optimize
- Distance calculation
	- euclidean
	- manhattan
	- chebyshev
	- minowski
- Sorting wrt distance and picking 1st K points
- Voting
	- Standard - Equal scheme
	- Weighted scheme