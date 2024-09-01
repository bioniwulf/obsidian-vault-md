---
date: 2024-09-01
title: A Quaternion-Based LOS Guidance Scheme for Path Following of AUVs
link: https://www.sciencedirect.com/science/article/pii/S1474667016461653
tags:
  - article
  - pathFollowing
  - quaternion
  - LOS
---
This paper presents a quaternion version of the well-known Line-of-Sight (LOS) guidance algorithm for marine applications. The transformation from Euler angles is achieved by exploiting the nature of the quaternion structure and using fundamental half-angle formulae from trigonometry. First, the Euler angles version of the LOS guidance algorithm is briefly presented for two uncoupled cases: a) the horizontal _xy_-plane, and b) the vertical _zx_-plane. Then, a coupled case is also considered and the transformation procedure is presented for all three cases. The vehicle considered pertains to a 5-DOF kinematics model where the roll angle is neglected, typical of torpedo-shaped Autonomous Underwater Vehicles (AUVs). Naturally, the Euler angles representation of the system involves singularities which, in the general 3-D space navigation case, should be avoided. The presented method aims at providing a singularity-free and computationally-efficient version of the conventional LOS algorithm.