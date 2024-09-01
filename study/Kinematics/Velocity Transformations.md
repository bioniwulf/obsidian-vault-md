---
date: 2024-09-01
tags:
  - theory
---
## Linear Transformations
The relationship between the NED linear velocity vector $\dot{\boldsymbol{p}}_{b/n}^n$ and the body-fixed velocity vector $\dot{\boldsymbol{p}}_{b/n}^n$ can be expressed in $\{n\}$ as
$$
\dot{\boldsymbol{p}}_{b/n}^n = \boldsymbol{R}_b^n(\boldsymbol{\Theta}_{nb})\boldsymbol{v}_{b/n}^b
$$
## Angular Transformations
The body-fixed angular velocity vector $\boldsymbol{\omega}_{b/n}^b = [p, q, r]$ and the Euler rate vector $\dot{\boldsymbol{\Theta}}_{nb} = [\dot{\phi}, \dot{\theta}, \dot{\psi}]$ ([[Euler Angle Transformation]])
related through a transformation matrix $\boldsymbol{T}_\Theta(\boldsymbol{\Theta}_{nb})$ according to
$$
\dot{\boldsymbol{\Theta}}_{nb} = \boldsymbol{T}_\Theta(\boldsymbol{\Theta}_{nb})\boldsymbol{\omega}_{b/n}^b
$$

where $\boldsymbol{T}_\Theta(\boldsymbol{\Theta}_{nb})$ is
$$
\displaystyle
\boldsymbol{T}_\Theta(\boldsymbol{\Theta}_{nb}) = 
\begin{bmatrix}
1 & \sin{\phi} \tan{\theta} & \cos{\phi} \tan{\theta} \\
0 & \cos{\phi} & -\sin{\phi} \\
0 & \displaystyle \frac{\sin{\phi}}{\cos{\theta}} & \displaystyle \frac{\cos{\phi}}{\cos{\theta}}
\end{bmatrix}
$$
The differential equation for the rotation matrix between the BODY and NED reference frames is
$$
\dot{\boldsymbol{R}}_b^n = \boldsymbol{R}_b^n \boldsymbol{S}(\boldsymbol{\omega}_{b/n}^b)
$$
where $\boldsymbol{S}(\boldsymbol{\omega}_{b/n}^b)$ is [[Skew-symmetric matrix]] and denotes as
$$
\boldsymbol{S}(\boldsymbol{\omega}_{b/n}^b) = 
\begin{bmatrix}
0 & -r & q \\
r & 0 & -p \\
-q & p & 0
\end{bmatrix}
$$