---
date: 2024-09-01
title: Line of Sight
tags:
  - theory
  - pathFollowing
---
# Line of Sight
The Line-of-Sight path following algorithm is one of most well-known algorithm of solving path following problem.
Firstly was introduced in the work [[Line‐of‐sight path following of underactuated marine craft]] by Thor Fossen.
## Overview (3D case)
The LOS method is similar to (Micaelli and Samson) in the sense that the ''reference point" is chosen as the orthogonal projection of the vehicle onto the path. Thus, the along track‐error $s_1(t) = 0$ for all $t$ . However, it is different in that it derives a control law for the vehicle's heading $\psi$  to achieve path following, instead of the heading rate $r$.
![[LOS schema.png]]
Control law for LOS method:
$$
\begin{matrix*}[l]
u=U_d \\
\displaystyle \psi = \psi_{\text{LOS}} = \psi_\mathcal{P}+\arctan{\left( -\frac{y_1}{\Delta_h} \right)}
\end{matrix*}
$$
where $\Delta_h$ is a tuning parameter (*look‐ahead* distance) and $\psi_{\text{LOS}}$ is called the light‐of‐sight angle that the heading of the vehicle should reach to achieve path following.
```pseudo
    \begin{algorithm}
    \caption{LOS pseudo-algorithm}
	    \begin{algorithmic}
		    \State For every time $t$ do:
			\Procedure{PFController}{}
				\State Find P — the point on the path closest to the vehicle
				\State For inner‐loop controllers:
				\State - Compute the desired vehicle's forward speed $u$
				\State - Compute the desired vehicle's yaw rate $\psi$
			\EndProcedure
	    \end{algorithmic}
    \end{algorithm}
```
## Notes
* $\Delta_h$ can be time varying and used to shape the convergence behavior towards the tangent (longitudinal) axis of $\{\mathcal{P}\}$.
* The larger value of $\Delta_h$ the slower will the convergence be, but this in turn will require less aggressive turning maneuvers in order for the vehicle to reach the path.
* The control law for $\psi$ can be rewritten in $\{\mathcal{B}\}$ as:
$$
\displaystyle  \psi_\mathcal{B} = \psi_e + \arctan{\left( -\frac{y_1}{\Delta_h} \right)}
$$
* There is quaternion-based approach of LOS algorithm presented in the paper [[A Quaternion-Based LOS Guidance Scheme for Path Following of AUVs]]