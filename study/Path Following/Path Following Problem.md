---
date: 2024-09-01
title: Path Following Problem
tags:
  - theory
  - pathFollowing
source: "[[A review of path following control strategies for autonomous robotic vehicles]]"
---
## Path Following Problem in 2D
**Let** $\mathcal{P}$ be a spatial path defined in an inertial frame and parametrized by a scalar variable γ (e.g., arc‐length of the path). Normally,  $\gamma \in \Omega := [a,b]$ where $a,b \in \mathbb{R}$ are values of $\gamma$ corresponding to the points at beginning and end of the path. The position of a generic point $P$ on the path in the inertial frame $\{n\}$ is described by vector
$$
\boldsymbol{\mathrm{p}}_{\mathrm{d}} = [\mathrm{x}_\mathrm{d}(\gamma), \mathrm{y}_\mathrm{d}(\gamma) ]^\intercal \in \mathbb{R}^2
$$
**Let** a kinematics model of a vehicle be described as follows (the simplest under-actuated case without external disturbance)
$$
\begin{matrix*}[l]
   \dot{x} = u \cos(\psi) \\
   \dot{y} = u \sin(\psi) \\
   \dot{\psi} = r
\end{matrix*}
$$
where:
* $[x,y]^\intercal$ is the position of the vehicle in $\{n\}$,
* $u$ is the longitudinal speed of the vehicle,
* $\psi$ is the heading of the vehicle,
* $r$ is heading rate.

**Given** the 2‐D spatial path $\mathcal{P}$ and a vehicle with the kinematics model derive a feedback control law for the vehicle's inputs ($u$ , $r$) and possibly for $\dot{\gamma}$  or $\ddot{\gamma}$ so as to fulfill the following tasks:
## Geometric task
Steer the position error $\boldsymbol{\mathrm{e}} \triangleq \boldsymbol{\mathrm{p}} - \boldsymbol{\mathrm{p}}_{\mathrm{d}}$ s.t.
$$

\lim\limits_{t \rightarrow \infty}{\boldsymbol{\mathrm{e}}(t)} = 0
$$
where $\boldsymbol{\mathrm{p}}_{\mathrm{d}}$ is the inertial position of a "reference point" $P$ on the path.
## Dynamic Task
Ensure that the vehicle's forward speed tracks a positive desired speed profile $\mathrm{U_d}=\mathrm{U_d}(t,\gamma)$, that is
$$
\lim\limits_{t \rightarrow \infty} \mathrm{u}(t) - \mathrm{U_d}(t) = 0
$$
This task can be reformulated as follows
$$
\lim\limits_{t \rightarrow \infty} \dot{\gamma}(t) - \mathrm{v_d}(\gamma, t) = 0
$$
where $\mathrm{v_d}(\gamma, t)$ is the desired speed profile, defined by
$$
\mathrm{v_d}(\gamma, t) \triangleq \frac{1}{\|\boldsymbol{\mathrm{p}}'_\mathrm{d}(\gamma)\|}\mathrm{U_d}(\gamma,t)
$$

In path following, the point $P$ on the path plays the role of a "reference point" for the vehicle to track. This point can be chosen as the nearest point to the vehicle (as in the paper [[Trajectory tracking for unicycle‐type and two‐steering‐wheels mobile robots]] or [[Line‐of‐sight path following of underactuated marine craft]]) that is, the orthogonal projection of the vehicle on the path (in case it is well defined), or can be initialized arbitrarily anywhere on the path with its evolution controlled through $\dot{\gamma}$ (as in paper [[Principles of guidance‐based path following in 2D and 3D]] or [[Nonlinear path following with applications to the control of autonomous underwater vehicles]]) or $\ddot{\gamma}$ (in paper [[Trajectory-Tracking and Path-Following of Underactuated Autonomous Vehicles With Parametric Modeling Uncertainty]]). 
## Path Description
At $P$, there are two frames adopted in the literature to formulate the path following problem, that is, to describe the position error between the vehicle and the path. Namely, the [[Frenet–Serret frame]] and the [[Parallel Transport frame]].
## Path Following Algorithms
See [[Path Following Algorithms]]