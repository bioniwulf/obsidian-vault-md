---
date: 2024-09-01
tags:
  - theory
  - kinematics
---
# Vehicle Kinematics
[[Handbook of Marine Craft Hydrodynamics and Motion Control]], Chapter 2.1

Kinematics treats only geometrical aspects of motion.

For marine craft moving in six **degrees of freedom** **(DOFs)**, six independent coordinates are necessary to determine the position and orientation. The first three coordinates, and their time derivatives, correspond to the position and translational motion along the $x$, $y$ and $z$ axes, while the last three coordinates and their time derivatives are used to describe orientation and rotational motion. For marine craft, the six different motion components are conveniently defined as *surge*, *sway*, *heave*, *roll*, *pitch* and *yaw* [[SNAME Notation]].

![[Pasted image 20240829111643.png]]
Crucial aspects of Kinematics:
* [[Reference frames]]
* [[Vectoral Notation]]
## Euler Angle Representation
### Vectoral Form (6DOF)
6DOF kinematic equations can be expressed in vector form as:
$$
\dot{\boldsymbol{\eta}} = \boldsymbol{J}_{\Theta}(\boldsymbol{\eta})\boldsymbol{\nu}
$$
or in equivalent form (according [[Velocity Transformations]])
$$
\begin{bmatrix}
\dot{\boldsymbol{p}_{b/n}^n} \\
\dot{\boldsymbol{\Theta}}_{nb}
\end{bmatrix}
=
\begin{bmatrix}
\boldsymbol{R}_b^n(\boldsymbol{\Theta}_{nb}) & \boldsymbol{0}_{0 \times 0} \\
\boldsymbol{0}_{0 \times 0} & \boldsymbol{T}_\Theta(\boldsymbol{\Theta}_{nb})
\end{bmatrix}
\begin{bmatrix}
\boldsymbol{v}_{b/n}^b \\
\boldsymbol{\omega}_{b/n}^b
\end{bmatrix}
$$

### Vectoral Form (3DOF)
Simplified representation of 3DOF (surge, sway and yaw) motion can be expressed as
$$
\dot{\boldsymbol{\eta}} = \boldsymbol{R}(\psi)\boldsymbol{\nu}
$$
where:
* $\boldsymbol{R}(\psi):=\boldsymbol{R}_{z,\psi}$
* $\boldsymbol{\nu}=[u,v,r]^\intercal$
* $\boldsymbol{\eta}=[N,E, \psi]^\intercal$