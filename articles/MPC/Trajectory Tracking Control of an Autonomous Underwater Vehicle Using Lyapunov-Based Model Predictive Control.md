---
date: 2024-09-03
title: Trajectory Tracking Control of an Autonomous Underwater Vehicle Using Lyapunov-Based Model Predictive Control
tags:
  - AUV
  - article
  - MPC
  - ThrusterAllocation
  - ROV
source: https://ieeexplore.ieee.org/document/8126875/
---
This paper studies the trajectory tracking control problem of an autonomous underwater vehicle (AUV). We develop a novel Lyapunov-based model predictive control (LMPC) framework for the AUV to utilize computational resource (online optimization) to improve the trajectory tracking performance. Within the LMPC framework, the practical constraints, such as actuator saturation, can be explicitly considered. Also, the thrust allocation subproblem can be addressed simultaneously with the LMPC controller design. Taking advantage of a nonlinear backstepping tracking control law, we construct the contraction constraint in the formulated LMPC problem so that the closed-loop stability is theoretically guaranteed. Sufficient conditions that ensure the recursive feasibility, and hence the closed-loop stability, are provided analytically. A guaranteed region of attraction is explicitly characterized. In the meantime, the robustness of the tracking control can be improved by the receding horizon implementation that is adopted in the LMPC control algorithm. Simulation results on the Saab SeaEye Falcon model AUV demonstrate the significantly enhance trajectory tracking control performance via the proposed LMPC method.