---
date: 2024-09-01
title: Coordinated Path Following Control of Multiple Wheeled Robots with Directed Communication Links
tags:
  - article
  - pathFollowing
  - GraphTheory
  - WheeledRobots
link: https://ieeexplore.ieee.org/document/1583303/
---
The paper addresses the problem of steering a fleet of wheeled robots along a set of given spatial paths, while keeping a desired inter-vehicle formation pattern. This problem arises for example when multiple vehicles are required to scan a given area in cooperation. In a possible mission scenario, one of the vehicles acts as a leader and follows a path accurately, while the other vehicles follow paths that are naturally determined by the formation pattern imposed. The solution adopted for coordinated path following builds on Lyapunov-based techniques and addresses explicitly the constraints imposed by the topology of the inter-vehicle communications network, which is captured in the framework of directed graph theory. With this set-up, path following (in space) and inter-vehicle coordination (in time) are essentially decoupled. Path following for each vehicle amounts to reducing a conveniently defined error variable to zero. Vehicle coordination is achieved by adjusting the speed of each of the vehicles along its path, according to information on the position of the other vehicles, as determined by the communications topology adopted. Simulations illustrate the efficacy of the solution proposed.