---
date: 2024-09-01
tags:
  - article
  - pathFollowing
  - MPC
  - UAV
  - ISS
link: https://onlinelibrary.wiley.com/doi/full/10.1002/rnc.4896
title: Cooperative path following of constrained autonomous vehicles with model predictive control and event-triggered communications
---
AMV, autonomous marine vehicle; CPF, cooperative path following; ETC, event-triggered communication; ISS, input-to-state-stable; MPC, model predictive control; UAVs, unmanned aerial vehicles.

We present a solution to the problem of multiple vehicle cooperative path following (CPF) that takes explicitly into account vehicle input constraints, the topology of the intervehicle communication network, and time-varying communication delays. The objective is to steer a group of vehicles along given spatial paths, at speeds that may be path dependent, while holding a feasible geometric formation. The solution involves decoupling the original CPF problem into two subproblems: (i) single path following of input-constrained vehicles and (ii) coordination of an input-constrained multiagent system. The first is solved by adopting a sampled-data model predictive control scheme, whereas the latter is tackled using a novel distributed control law with an event-triggered communication (ETC) mechanism. The proposed strategy yields a closed-loop CPF system that is input-to-state-stable with respect to the system's state (consisting of the path following error of all vehicles and their coordination errors) and the system's input, which includes triggering thresholds for ETC communications and communication delays. Furthermore, with the proposed ETC mechanism, the number of communications among the vehicles are significantly reduced. Simulation examples of multiple autonomous vehicles executing CPF maneuvers in 2D under different communication scenarios illustrate the efficacy of the CPF strategy proposed.