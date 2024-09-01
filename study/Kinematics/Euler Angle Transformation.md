---
date: 2024-09-01
tags:
  - theory
  - kinematics
---
[[Handbook of Marine Craft Hydrodynamics and Motion Control]], Chapter 2.2.1
The Euler angles, roll ($\phi$) , pitch ($\theta$) and yaw ($\psi$), can now be used to decompose the body-fixed velocity
vector $\boldsymbol{v}_{b/n}^b$ in the NED reference frame. Let $\boldsymbol{R}_b^n(\boldsymbol{\Theta}_{nb}): \mathcal{S}^3 \rightarrow SO(3)$  denote the Euler angle rotation
matrix with argument $\boldsymbol{\Theta}_{nb} = [\phi, \theta, \psi]^\intercal$. Hence,
$$
\boldsymbol{v}_{b/n}^n = \boldsymbol{R}_b^n(\boldsymbol{\Theta}_{nb}) \boldsymbol{v}_{b/n}^b
$$It is customary to describe $\boldsymbol{R}_b^n(\boldsymbol{\Theta}_{nb})$ by three principal rotations about the $z$, $y$ and $x$ axes ($zyx$ convention).
Note that the order in which these rotations is carried out is **not arbitrary**. In guidance, navigation and
control applications it is common to use the $zyx$ convention from $\{n\}$ to  $\{b\}$ specified in terms of the Euler
angles $\phi$, $\theta$ and $\psi$ for the rotations.
This rotation sequence is mathematically equivalent to
$$
\boldsymbol{R}_b^n(\boldsymbol{\Theta}_{nb}):=\boldsymbol{R}_{z,\psi}\boldsymbol{R}_{y,\theta}\boldsymbol{R}_{x,\phi}
$$
and the inverse transformation is then written ($zyx$ convention)
$$
\boldsymbol{R}_b^n(\boldsymbol{\Theta}_{nb})^\intercal = \boldsymbol{R}_n^b(\boldsymbol{\Theta}_{nb})=\boldsymbol{R}_{x,\phi}^\intercal\boldsymbol{R}_{y,\theta}^\intercal\boldsymbol{R}_{z,\psi}^\intercal
$$

The principal rotation around axis $x, y, z$ denotes as follows
$$
\boldsymbol{R}_{x,\phi} = 
\begin{bmatrix}
1 & 0 & 0 \\
0 & \cos{\phi} & -\sin{\phi} \\
0 & \sin{\phi} & \cos{\phi} \\
\end{bmatrix},
\boldsymbol{R}_{y,\theta} = 
\begin{bmatrix}
\cos{\theta} & 0 & \sin{\theta} \\
0 & 1 & 0 \\
-\sin{\theta} & 0 & \cos{\theta} \\
\end{bmatrix},
\boldsymbol{R}_{z,\psi} = 
\begin{bmatrix}
\cos{\psi} & -\sin{\psi} & 0 \\
\sin{\psi} & \cos{\psi} & 0 \\
0 & 0 & 1 \\
\end{bmatrix},
$$