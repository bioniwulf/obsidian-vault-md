---
date: 2024-09-03
title: Experimental Evaluation on Depth Control Using Improved Model Predictive Control for AutonomousU nderwater Vehicle (AUVs)
link: https://www.mdpi.com/1424-8220/18/7/2321
tags:
  - article
  - MPC
  - AUV
---
Due to the growing interest using model predictive control (MPC), there are more and more researches about the applications of MPC on autonomous underwater vehicle (AUV), and these researches are mainly focused on simulation and simple application of MPC on AUV. This paper focuses on the improvement of MPC based on the state space model of an AUV. Unlike the previous approaches using a fixed weighting matrix, in this paper, a coefficient, varied with the error, is introduced to adjust the control increment vector weighting matrix to reduce the settling time. Then, an analysis on the effect of the adjustment to the stability is given. In addition, there is always a lag between the AUV real trajectory and the desired trajectory when the AUV tracks a continuous trajectory. To solve this problem, a simple re-planning of the desired trajectory is developed. Specifically, the point certain steps ahead from current time on the desired trajectory is treated as the current desired point and input to the controller. Finally, experimental results for depth control are given to demonstrate the feasibility and effectiveness of the improved MPC. Experimental results show that the method of real-time adjusting control increment weighting matrix can reduce settling time by about 2 s when tracking step trajectory of 1 m, and the simple re-planning of the desired trajectory method can reduce the average of absolute error by about 15% and standard deviation of error by about 17%.