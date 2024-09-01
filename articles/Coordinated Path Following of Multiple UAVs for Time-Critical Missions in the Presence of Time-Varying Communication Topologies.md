---
date: 2024-09-01
title: Coordinated Path Following of Multiple UAVs for Time-Critical Missions in the Presence of Time-Varying Communication Topologies
tags:
  - article
  - pathFollowing
  - GroupControl
  - DynamicCommunicationNetworks
link: https://www.sciencedirect.com/science/article/pii/S1474667016415715
---
We address the problem of steering multiple unmanned air vehicles (UAVs) along given paths (path-following) under strict temporal coordination constraints requiring, for example, that the vehicles arrive at their final destinations at exactly the same time. Path-following relies on a nonlinear Lyapunov based control strategy derived at the kinematic level with the augmentation of existing autopilots with ℒ1 adaptive output feedback control laws to obtain inner-outer loop control structures with guaranteed performance. Multiple vehicle time-critical coordination is achieved by enforcing temporal constraints on the speed profiles of the vehicles along their paths in response to information exchanged over a dynamic communication network. We consider that each vehicle transmits its coordination state to only a subset of the other vehicles, as determined by the communications topology adopted. We address explicitly the case where the communication graph that captures the underlying communication network topology may be disconnected during some interval of time (or may even fail to be connected at any instant of time) and provide conditions under which the closed-loop system is stable. Flight test results obtained at Camp Roberts, CA in 2008 and hardware-in-the-loop (HITL) simulations demonstrate the benefits of the algorithms developed.