---
date: 2024-08-20
tags:
  - article
title: "A review of path following control strategies for autonomous robotic vehicles: Theory, simulations, and experiments"
link: https://onlinelibrary.wiley.com/doi/full/10.1002/rob.22142
---
##  Article Notations

| Notation                                                                                                                                             | Description                                                                                                                |
| ---------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------- |
| $Q$                                                                                                                                                  | vehicle centre of mass                                                                                                     |
| $\{\mathcal{I}\} = \{x_I , y_I \}$                                                                                                                   | inertial (global) North‐East (NE) frame                                                                                    |
| $\{\mathcal{B}\} = \{x_b, y_b\}$                                                                                                                     | vehicle body fixed frame with $Q$ in the centre                                                                            |
| $\{\mathcal{P}\} = \{x_p, y_p\}$                                                                                                                     | path frame                                                                                                                 |
| $\gamma$                                                                                                                                             | the scalar parameter for description of the path (e.g., arc‐length of the path)                                            |
| $\mathrm{v}_\gamma=\dot{\gamma}$                                                                                                                     | the velocity of $\gamma$ ==????==                                                                                          |
| $\displaystyle \mathrm{v}_d \triangleq \frac{1}{\|\boldsymbol{p}'_d(\gamma)\|}U_d(\gamma, t)$                                                        | the desired speed profile for $\dot{\gamma}$                                                                               |
| $\boldsymbol{p}_d(\gamma)=[x_d(\gamma), y_d(\gamma)]^⊤$                                                                                              | desired path points in $\{\mathcal{I}\}$ parameterised by $\gamma$                                                         |
| $\boldsymbol{p} = [x, y]^{\intercal}$                                                                                                                | vehicle position in $\{\mathcal{I}\}$                                                                                      |
| $\psi$                                                                                                                                               | vehicle heading in $\{\mathcal{I}\}$                                                                                       |
| $\boldsymbol{\mathrm{v}} = [u, v]^{\intercal}$                                                                                                       | vehicle longitudinal (surge) and lateral (sway) velocity with respect to the fluid in $\{\mathcal{B}\}$                    |
| $\boldsymbol{v_c} = [v_{cx}, v_{cy}]^{\intercal}$                                                                                                    | external unknown disturbances (e.g., ocean current in the case of marine vehicles and wind in the case of aerial vehicles) |
| $\displaystyle \psi_{\mathcal{P}} = \arctan \left( \frac{y'_d(\gamma)}{x'_d(\gamma)} \right)$                                                        | tangent angle of the path at point $\gamma$ expressed in the $\{\mathcal{I}\}$                                             |
| $\boldsymbol{e}_p \triangleq [s_1, y_1]^{\intercal}$                                                                                                 | the position error between the vehicle and the reference point $P$                                                         |
| $\boldsymbol{e}_\mathcal{B}=\boldsymbol{R}^{\mathcal{B}}_{\mathcal{I}}(\boldsymbol{p}-\boldsymbol{p_d})$                                             | the position error between the vehicle and the path in the $\{\mathcal{B}\}$                                               |
| $e_\gamma$                                                                                                                                           | the tracking error for the speed of the path parameter                                                                     |
| $\boldsymbol{\epsilon} \triangleq [\epsilon_1, \epsilon_2]^{\intercal}$                                                                              | arbitrarily small nonzero constant vector                                                                                  |
| $s_1, y_1$                                                                                                                                           | along‐track and cross‐track errors, respectively                                                                           |
| $\psi_e = \psi - \psi_\mathcal{P}$                                                                                                                   | the orientation error between the vehicle's heading and the tangent to the path                                            |
| $k(\gamma)=\| \boldsymbol t'(\gamma) \|$                                                                                                             | the curvature of the path                                                                                                  |
| $\displaystyle \boldsymbol{t}(\gamma) = \frac{\boldsymbol p'_d(\gamma)}{\|\boldsymbol p'_d(\gamma\|}$                                                | unit tangent vector respectively to the path                                                                               |
| $\displaystyle \boldsymbol{n}(\gamma) = \frac{\boldsymbol t'(\gamma)}{\|\boldsymbol t'(\gamma\|}$                                                    | principle unit normal respectively to the path                                                                             |
| $U_d(t)$                                                                                                                                             | positive desired longitudinal speed of the vehicle                                                                         |
| $u_{\mathcal{P}} = \dot{\boldsymbol{p_d}}= \|\boldsymbol{p}'_d(\gamma)\|\dot{\gamma}$                                                                | the velocity of reference point $P$ with respect to the $\{\mathcal{I}\}$ ==Longitudal?==                                  |
| $\boldsymbol{w}_\mathcal{P} = [r_\mathcal{P}, 0]^\intercal$                                                                                          | the angular velocity vector of $\{ \mathcal{P} \}$ respect to $\{ \mathcal{I} \}$ expressed in $\{ \mathcal{P} \}$         |
| $\boldsymbol{\mathrm{v}}_{\mathcal{P}} \triangleq [u_{\mathcal{P}}, 0]^{\intercal}=\boldsymbol{R}^{\mathcal{P}}_{\mathcal{I}}\dot{\boldsymbol{p_d}}$ | the velocity of reference point $P$ with respect to $\{\mathcal{I}\}$, expressed in $\{\mathcal{P}\}$ ==???==              |
| $\boldsymbol{\mathrm{u}}_{\mathcal{P}} \triangleq [r, \mathrm{v}_\gamma]^{\intercal}$                                                                | the velocity of reference point $P$ with respect to $\{\mathcal{P}\}$ ==????==                                             |
| $\boldsymbol{\mathrm{w}}=[r,0]^\intercal$                                                                                                            | the angular velocity vector of $\{\mathcal{B}\}$ respect to $\{I\}$ expressed in $\{\mathcal{B}\}$                         |
| $\boldsymbol{\mathrm{u}}=[u,r]$                                                                                                                      | the vehicle linear and angular velocity in $\{\mathcal{B}\}$                                                               |
| $\boldsymbol{\mathrm{x}} = \left[ \boldsymbol{e}^\intercal_{\mathcal{B}}, e_\gamma \right]^\intercal \in \mathbb{R}^3$                               | The complete path following error in $\{\mathcal{B}\}$                                                                     |
| $r_{\mathcal{P}}=\dot{\psi}_{\mathcal{P}}=k(\gamma)u_{\mathcal{P}}$                                                                                  | the angular velocity vector of $\{\mathcal{P}\}$ respect to $\{I\}$ expressed in $\{\mathcal{P}\}$                         |
| $\displaystyle v_d(\gamma,t) \triangleq \frac{1}{\|\boldsymbol{p}'_d(\gamma)\|}U_d(\gamma, t)$                                                       | desired speed profile for $\dot{\gamma}$                                                                                   |
| $R^{\mathcal{P}}_{\mathcal{I}}$                                                                                                                      | Rotation matrix from $\{\mathcal{P}\}$ to $\{\mathcal{I}\}$                                                                |
| $R^{\mathcal{B}}_{\mathcal{I}}$                                                                                                                      | Rotation matrix from $\{\mathcal{B}\}$ to $\{\mathcal{I}\}$                                                                |
## Article Links
* [Path Following Algorithm Matlab](https://github.com/hungrepo/path-following-Matlab/tree/master/PF-toolbox)
* [Path Following Algorithm C++ ROS](https://github.com/dsor-isr/Paper-PathFollowingSurvey)
* [Modelling video](https://youtu.be/XutfsXijHPE.)
## Article Questions
* (page 7, eq. 11) Why the norm is placed in the equation? (chain rule for the derivative of the composition of two differentiable functions)
* (page 7, eq. 13) What is the physical meaning of desired speed profile variable $v_d(\gamma, t)$? Why is it obtained by dividing by the norm of derivative function of $\boldsymbol{p}(\gamma)$ with respect to gamma?
* (page 8, eq. 18) I got intuitively this function, but how it was obtained?
* (page 10, eq 30) Was this function was obtained somehow or just defined and proved that this is the solution?
* (page 12, eq 38) What is the point to use this equation instead of eq 35? Is convergence waster or is it faster to calculate?
* (page 13, eq 39) What is $v_\gamma$ ?
## Article Notes
* there are two frames adopted in the literature to formulate the path following problem, that is, to describe the position error between the vehicle and the path. Namely, the [[Frenet–Serret frame]](F-S) frame ([link](https://sakshik.medium.com/understanding-the-frenet-serret-frame-3b9c730e8b1c)) and the [[Parallel Transport frame]] (P‐T) frame.
* **(F‐S)** frame is that it is not well‐defined for paths that have a vanishing second derivative (i.e., zero curvature) such as straight lines or nonconvex curves.
* tangent basic vector in **(P‐T)** is the same as in **(F‐S)**, but normal vector is obtained by rotating the tangent vector 90 clockwise.
## Problem Formulation
### Vehicle Kinematics Model (2D Case)
#### Fully-Actuated Vehicle's with External Disturbances
$$
\begin{matrix*}[l]
   \dot{x} = u \cos(\psi) - v\sin{\psi} + v_{cx} \\
   \dot{y} = u \sin(\psi) + v \cos{\psi} + v_{cy} \\
   \dot{\psi} = r
\end{matrix*}
$$
#### Under-Actuated Vehicle's without External Disturbances
$$
\begin{matrix*}[l]
   \dot{x} = u \cos(\psi) \\
   \dot{y} = u \sin(\psi) \\
   \dot{\psi} = r
\end{matrix*}
$$
#### Under-Actuated Vehicle's with External Disturbances
$$
\begin{matrix*}[l]
   \dot{x} = u \cos(\psi) + v_{cx} \\
   \dot{y} = u \sin(\psi) + v_{cy} \\
   \dot{\psi} = r
\end{matrix*}
$$
#### Fully-Actuated Vehicle's without External Disturbances
$$
\begin{matrix*}[l]
   \dot{x} = u \cos(\psi) - v\sin{\psi} \\
   \dot{y} = u \sin(\psi) + v \cos{\psi} \\
   \dot{\psi} = r
\end{matrix*}
$$
### Path Following Error in $\{\mathcal{P}\}$ ( [[#### Under-Actuated Vehicle's without External Disturbances]] case)
Let $P$ be a point moving along the path that plays the role of a reference point for the vehicle to track so as to achieve path following. Let $\mathcal{P}$ be the [[Parallel Transport frame]] frame attached to this point defined by rotating the inertial frame by angle $\psi_\mathcal{P}$, where $\psi_\mathcal{P}$ is the angle that the tangent
vector at $P$ makes with $x_\mathcal{I}$
With notations expressed above path following error in $\{\mathcal{P}\}$:
$$
\boldsymbol{e}_\mathcal{P}=\boldsymbol{R}^{\mathcal{P}}_{\mathcal{I}}(\psi_\mathcal{P})(\boldsymbol{p}-\boldsymbol{p_d})
$$
Where $\boldsymbol{R}^{\mathcal{P}}_{\mathcal{I}}$:
$$
\boldsymbol{R}^{\mathcal{P}}_{\mathcal{I}} = 
\begin{bmatrix}
\cos{\psi_\mathcal{P}} & \sin{\psi_\mathcal{P}} \\
-\sin{\psi_\mathcal{P}} & \cos{\psi_\mathcal{P}}
\end{bmatrix}
$$
**The dynamics of the position error in $\{P\}$ as well as dynamics of the error orientation could be rewritten as follows:**
$$
\begin{matrix*}[l]
\dot{\boldsymbol{e}}_\mathcal{P} = -\boldsymbol{S}(\boldsymbol{w_p})\boldsymbol{e}_\mathcal{P} +
\begin{bmatrix}
u\cos{\psi_e} \\
u\sin{\psi_e}
\end{bmatrix}
-
\begin{bmatrix}
u_\mathcal{P} \\
0
\end{bmatrix} \\
\dot{\psi}_e = r - k(\gamma) u_\mathcal{P}
\end{matrix*}
$$
where $\boldsymbol{S}(\boldsymbol{w_\mathcal{P}})$ is skew  symmetric matrix parameterized by $\boldsymbol{w}_\mathcal{P}=[r_\mathcal{P},0]$:
$$
\boldsymbol{S}(\boldsymbol{w_\mathcal{P}})=
\begin{bmatrix}
0 & -r_\mathcal{P} \\
r_\mathcal{P} & 0
\end{bmatrix}
$$
where $r_\mathcal{P}$ is the angular velocity vector of $\{\mathcal{P}\}$ respect to $\{I\}$ expressed in $\{\mathcal{P}\}$.
$r_P$ satisfies the relation:
### Path Following Error in $\{\mathcal{B}\}$
![[Pasted image 20240825173239.png]]
let $P$, whose coordinate is specified by $\boldsymbol{p}_d(\gamma)$, be the "reference point" on the path that the vehicle should track to achieve path following. Define
$$
\boldsymbol{e}_\mathcal{B}=\boldsymbol{R}^{\mathcal{B}}_{\mathcal{I}}(\boldsymbol{p}-\boldsymbol{p_d})-\boldsymbol{\epsilon}
$$
as the position error between the vehicle and the path resolved in the vehicle's body frame $\{\mathcal{B}\}$, where $\epsilon$ is an arbitrarily small nonzero constant vector and
$$
\boldsymbol{R}^{\mathcal{B}}_{\mathcal{I}} = 
\begin{bmatrix}
\cos{\psi} & \sin{\psi} \\
-\sin{\psi} & \cos{\psi}
\end{bmatrix}
$$

Let $\boldsymbol{\mathrm{x}} = \left[ \boldsymbol{e}^\intercal_{\mathcal{B}}, e_\gamma \right]^\intercal \in \mathbb{R}^3$ be the complete path following error vector, then the dynamics of the path following error vector can be expressed as
$$
\dot{\boldsymbol{\mathrm{x}}} =
\begin{bmatrix}
-S(\boldsymbol{\mathrm{w}})\boldsymbol{e}_\mathcal{B} + \Delta\boldsymbol{\mathrm{u}}-R^\mathcal{B}_\mathcal{I}(\psi)\boldsymbol{p}'_d(\gamma)\dot{\gamma} \\
\ddot{\gamma} - \dot{\mathrm{v}}_d
\end{bmatrix}
$$
where $\Delta$ expressed as
$$
\Delta = 
\begin{bmatrix}
1 & \epsilon_2 \\
0 & \epsilon_1
\end{bmatrix}
$$
## Methods Overview

| PF methods                                | Drive $\boldsymbol{e}_P$ to zero by | References                                                                                                                                                | External disturbances |
| ----------------------------------------- | ----------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------- |
| [[### Method 1 (Micaelli and Samson)]]    | $u,r$                               | Micaelli and Samson ([1993](https://inria.hal.science/inria-00074575/document))                                                                           |                       |
| [[### Method 2 (Lapierre et al)]]         | $u,r, \dot{\gamma}$                 | Lapierre et al. ([2003](https://ieeexplore.ieee.org/stamp/stamp.jsp?arnumber=1272781))                                                                    |                       |
| [[### Method 3 (LOS path following)]]     | $u,\psi$                            | Fossen et al. ([2003](https://www.sciencedirect.com/science/article/pii/S1474667017378096), [2015](https://ieeexplore.ieee.org/document/6868251))         | supports              |
| [[### Method 4 (Breivik & Fossen, 2005)]] | $u,\psi, \dot{\gamma}$              | Breivik and Fossen ([2005](https://ieeexplore.ieee.org/document/1582226))                                                                                 |                       |
| [[### Method 5 (Hung et al., NMPC)]]      | $u,r, \dot{\gamma}$                 | Hung et al. ([2020](https://onlinelibrary.wiley.com/doi/full/10.1002/rnc.4896)), Yu et al. ([2015](https://onlinelibrary.wiley.com/doi/10.1002/rnc.3133)) |                       |
**Table. Methods proposed to stabilize $\boldsymbol{e}_{\mathcal{P}}$ to zero

| PF methods                                 | Drive $\boldsymbol{e}_{\mathcal{B}}$ to zero by | References                                                                   | External disturbances |
| ------------------------------------------ | ----------------------------------------------- | ---------------------------------------------------------------------------- | --------------------- |
| [[### Method 6 (Aguiar & Hespanha, 2007)]] | $u,r, \ddot{\gamma}$                            | Aguiar & Hespanha ([2007](https://www.mdpi.com/2077-1312/11/10/1874))        | supports              |
| [[### Method 7 (Hung et al., 2020, NMPC)]] | $u,r, \dot{\gamma}$                             | Alessandretti et al., ([2013](https://ieeexplore.ieee.org/document/6669717)) |                       |
**Table. Methods proposed to stabilize $\boldsymbol{e}_{\mathcal{B}}$ to zero
## Methods Chronology
![[Pasted image 20240823153409.png||1200]]

## Methods Detailed Description
### Method 1 (Micaelli and Samson)
[[## Methods Overview]]
**Controlled variables**: $u,r$
**Type**: Path frame

In this method, the reference point $P$ is chosen as the orthogonal projection of the real vehicle on the path, that is, the point on the path closest to the vehicle (if it is well‐defined). With this strategy the along‐track error is always zero, that is, $s_1(t)=0$.
In this case, the dynamics of the cross‐track error can be written explicitly as:
$$
\begin{matrix*}[l]
\dot{y_1}= -r_Ps_1+u\sin{\psi_e}=u\sin{\psi_e}\\
\dot{\tilde{\psi}} = r - k(\gamma)u_P - \dot{\delta}
\end{matrix*}
$$
where:
* $\delta(y_1,u)$  is a time differentiable design function that can be used to shape the manner in which the vehicle approaches the path,
* $\tilde{\psi} = \psi_e - \delta(y_1,u)$
**Condition for $\delta(y_1,u)$:**
* $\delta(0,u)=0$ for all $u$
* $y_1u\sin{\delta(y_1,u)} \leq 0$ for all $y_1,u$.

**So,  $u, r$ can be calculated as follows:**
$$
\begin{matrix*}[l]

u=U_d \\
\displaystyle r = k(\gamma)u_\mathcal{P}+\dot{\delta}-k_1\tilde{\psi} - k_2y_1u\frac{\sin{\psi_e} - \sin{\delta}}{\tilde{\psi}}
\end{matrix*}
$$
where $k_1, k_2$ are tuning parameters and $u_\mathcal{P}$ is defined as:
$$
u_\mathcal{P} = u\frac{\cos{\psi_e}}{1 - k(\gamma)y_1}
$$
The function $\delta(y_1,u)$ can be chosen as follows:
$$
\delta(y_1,u) = -\theta \tanh(k_{\delta}y_1u)
$$
where $\theta \in (0, \pi/2), k_{\delta}>0$
```pseudo
    \begin{algorithm}
    \caption{Method 1}
	    \begin{algorithmic}
		    \State For every time $t$ do:
			\Procedure{PFController}{}
				\State Find P — the point on the path closest to the vehicle
				\State Compute $y_1$, $\psi_e$, and $\tilde{\psi}$
				\State For inner‐loop controllers:
				\State - Compute the desired vehicle's forward speed $u$
				\State - Compute the desired vehicle's yaw rate given $r$
			\EndProcedure
	    \end{algorithmic}
    \end{algorithm}
```
**Notes**:
* Because the reference point $R$ on the path for the vehicle to track is chosen closest to the vehicle, there exists a singularity when $y_1= 1 / k(\gamma)$.
### Method 2 (Lapierre et al)
[[## Methods Overview]]
**Controlled variables**: $u,r, \dot{\gamma}$
**Type**: Path frame
This method uses the same controller for $u, r$ as in [[### Method 1 (Micaelli and Samson)]]:
$$
\begin{matrix*}[l]
u=U_d \\
\displaystyle r = k(\gamma)u_\mathcal{P}+\dot{\delta}-k_1\tilde{\psi} - k_2y_1u\frac{\sin{\psi_e} - \sin{\delta}}{\tilde{\psi}}
\end{matrix*}
$$
but $u_\mathcal{P}$ defines in it's own way:
$$
u_\mathcal{P} = u\cos{\psi_e} + k_3s_1
$$
where is $k_3>0$ is the additional tuning parameter.
```pseudo
    \begin{algorithm}
    \caption{Method 2}
	    \begin{algorithmic}
		    \State Initialize $\gamma(0)$
		    \State For every time $t$ do:
			\Procedure{PFController}{}
				\State Compute the position $e_{\mathcal{P}}$ and the orientation $\psi_e$ errors
				\State For inner‐loop controllers:
				\State - Compute the desired vehicle's forward speed $u$
				\State - Compute the desired vehicle's yaw rate $r$
				\State Compute $\dot{\gamma}$, integrate, and update $\gamma$
			\EndProcedure
	    \end{algorithmic}
    \end{algorithm}
```
**Notes**:
* The control law for $u_\mathcal{P}$  in implies that if the vehicle is behind/ahead of the reference point ($s_1 < 0 / s_1 > 0$) then the reference point decreases/increases its speed.
* Compared with [[### Method 1 (Micaelli and Samson)]] this strategy has the following advantages: **(i)** it doesn't require an algorithm to find a point on the path that is closest to the vehicle and **(ii)** it avoids the singularity that occurs in in the previous method.
### Method 3 (LOS path following)
[[## Methods Overview]]
**Controlled variables**: $u,\psi$
**Type**: Path frame
The LOS method is similar to [[#Method 1 (Micaelli and Samson)]] in the sense that the ''reference point" is chosen as the orthogonal projection of the vehicle onto the path. Thus, the along track‐error $s_1(t) = 0$ for all $t$ . However, it is different in that it derives a control law for the vehicle's heading $\psi$  to achieve path following, instead of the heading rate $r$.
![[Pasted image 20240826180939.png]]
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
    \caption{Method 3}
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
**Notes**:
* $\Delta_h$ can be time varying and used to shape the convergence behavior towards the tangent (longitudinal) axis of $\{\mathcal{P}\}$.
* The larger value of $\Delta_h$ the slower will the convergence be, but this in turn will require less aggressive turning maneuvers in order for the vehicle to reach the path.
* The control law for $\psi$ can be rewritten in $\{\mathcal{B}\}$ as:
$$
\displaystyle  \psi_\mathcal{B} = \psi_e + \arctan{\left( -\frac{y_1}{\Delta_h} \right)}
$$
### Method 4 (Breivik & Fossen, 2005)
[[## Methods Overview]]
**Controlled variables**: $u,\psi, \dot{\gamma}$
**Type**: Path frame

The idea behind this method is quite similar to that in [[#Method 2 (Lapierre et al)]]; however, instead of achieving path following by controlling the heading rate $r$, the authors propose a control law for $\psi$ similar to the [[#Method 3 (LOS path following)]]. Overall, the control law is follows:
$$
\begin{matrix*}[l]
u=U_d \\
\displaystyle \psi = \psi_\mathcal{P}+\arctan{\left( -\frac{y_1}{\Delta_h} \right)} \\
u_\mathcal{P} = u\cos{\psi_e} + k_1s_1
\end{matrix*}
$$
where:
* $k_1$ is regularization parameter to control speed of $\gamma$.
```pseudo
    \begin{algorithm}
    \caption{Method 4}
	    \begin{algorithmic}
		    \State Initialize $\gamma(0)$
		    \State For every time $t$ do:
			\Procedure{PFController}{}
				\State Compute the position errors $s_1, y_1$
				\State For inner‐loop controllers:
				\State - Compute the desired vehicle's forward speed $u$
				\State - Compute the desired vehicle's yaw $\psi$
				\State Compute $\dot{\gamma}$, integrate, and update $\gamma$
			\EndProcedure
	    \end{algorithmic}
    \end{algorithm}
```
**Notes**:
* $e_\mathcal{P}=0$ is UGAS (Uniform Global Asymptotic Stability) in this control method.
### Method 5 (Hung et al., NMPC)
[[## Methods Overview]]
**Controlled variables**: $u,r, \dot{\gamma}$
**Type**: Path frame

To deal with the vehicle's constraints explicitly, the optimization based control control strategy called model predictive control (MPC) can be used.
Fist, it's necessary to define control state for MPC:
$$
\boldsymbol{\mathrm{x}} = \left[ \boldsymbol{e}^\intercal_{\mathcal{P}}, \psi_e, \gamma \right]^\intercal \in \mathbb{R}^4
$$

The dynamics of the system can be rewritten as
$$
\dot{\boldsymbol{\mathrm{x}}}_\mathcal{P} =
\boldsymbol{\mathrm{f}}(\boldsymbol{\mathrm{x}}_\mathcal{P}, \boldsymbol{\mathrm{u}}_\mathcal{P})
\triangleq
\begin{bmatrix}
-\|\boldsymbol{p}'(\gamma)\|v_\gamma(1 - k(\gamma)y_1)+U_d\cos{\psi+e} \\
-k(\gamma)s_1\|\boldsymbol{p}'(\gamma)\|v_\gamma+U_d\sin{\psi_e} \\
r - k(\gamma)\|\boldsymbol{p}'(\gamma)\|v_\gamma \\
v_\gamma
\end{bmatrix}
$$
where $\boldsymbol{\mathrm{u}}_\mathcal{P} \triangleq [r, v_\gamma]$ is the input of the system , which is constrained in the set $\mathbb{U}_\mathcal{P}$ given by:
$$
\mathbb{U}_\mathcal{P} = \{(r,v_\gamma):
v_{\text{min}} \leq v_\gamma \leq v_{\text{max}}, |r|<r_\text{max}\}
$$

In this case a finite horizon open loop optimal control problem (FOCP-1) that the MPC solves at every sampling time as follows:
$$
\begin{matrix}
\min{J_\mathcal{P}(\boldsymbol{\mathrm{x}}_\mathcal{P},\bar{\boldsymbol{u}}_\mathcal{P}(\cdot))} \\
\textbf{subject to} \\
\dot{\boldsymbol{\mathrm{x}}}_\mathcal{P}(\tau) = \boldsymbol{\mathrm{f}}_\mathcal{P}(\bar{\boldsymbol{\mathrm{x}}}_\mathcal{P}(\tau), \bar{\boldsymbol{\mathrm{u}}}_\mathcal{P}(\tau)), \tau \in [t, t + T_p], \\
\bar{\boldsymbol{\mathrm{x}}}_\mathcal{P}(\tau) = \boldsymbol{\mathrm{x}}_\mathcal{P}(\tau), \\
(\bar{\boldsymbol{e}}_\mathcal{P}, \bar{\psi}_e(\tau)) \in \mathbb{E}_\mathcal{P}, \tau \in [t, t + T_p] \\
\textbf{with} \\
\displaystyle J_\mathcal{P}(\boldsymbol{\mathrm{x}}_\mathcal{P},\bar{\boldsymbol{u}}_\mathcal{P}(\cdot))
\triangleq
\int^{t+T_p}_{t}
\left\lVert
\begin{bmatrix}
	\bar{\boldsymbol{e}}_\mathcal{P}(\tau) \\
	\bar{\psi}_e(\tau)
\end{bmatrix}
\right\lVert_Q
+
\left\lVert
\bar{\boldsymbol{u}}_a(\tau)
\right\lVert_R d\tau
+
F_\mathcal{P}(\bar{\boldsymbol{e}}_\mathcal{P}(t+T_p), \bar{\psi}_e(t+T_p))
\end{matrix},
$$
where:
* $Q \in \mathbb{R}^{3\times3}, R \in \mathbb{R}^{2\times2}$ are positive definite matrices,
* notation $\left\lVert \boldsymbol{\mathrm{x}} \right\lVert = \boldsymbol{\mathrm{x}}^\intercal Q \boldsymbol{\mathrm{x}}$
* $\bar{\boldsymbol{\mathrm{x}}}_\mathcal{P}(\tau)$ is the predicted trajectory of the state $\boldsymbol{\mathrm{x}}_\mathcal{P}$ computed using the dynamic model
* $\boldsymbol{u}_a$ is the cost associated with the input that is defined as
$$
\boldsymbol{u}_a =
\begin{bmatrix}
U_d\cos{\psi_e - \| \boldsymbol{\mathrm{p}}'_d (\gamma) \| v_\gamma} \\
r - k(\gamma) \| \boldsymbol{\mathrm{p}}'_d (\gamma) \| v_\gamma
\end{bmatrix}
$$
In the MPC scheme, the FOCP‐1 is repeatedly solved at every discrete sampling instant $t_i=iT_s, i \in \mathbb{N}_+$ where $T_s$ is sampling interval. Let $\bar{\mathrm{\boldsymbol{u}}}^*_\mathcal{P}, \tau \in [t, t + T_p]$ be the optimal solution of the FOCP-1. Then the **MPC control law** $\boldsymbol{u}_\mathcal{P}(\cdot)$ is defined by
$$
\boldsymbol{u}_\mathcal{P}(t) = \bar{\mathrm{\boldsymbol{u}}}^*_\mathcal{P}, \tau \in [t_i, t_i + T_s]
$$
```pseudo
    \begin{algorithm}
    \caption{Method 5}
	    \begin{algorithmic}
		    \State Initialize $\gamma(0)$
		    \State For every time $t$ do:
			\Procedure{PFController}{}
				\State Compute the position errors $s_1, y_1, \psi_e$
				\State the FOCP and apply the MPC contol Law to obtain optimal $r, v_\gamma$
				\State For inner‐loop controllers:
				\State - Compute the desired vehicle's forward speed $u$
				\State - The optimal $r$ is used as the desired vehicle's heading rate
				\State Iterate $\gamma$ with the optimal input $v_\gamma$ to update $\gamma$
			\EndProcedure
	    \end{algorithmic}
    \end{algorithm}
```
**Notes**:
* While using the terminal constraints and the contractive constraint are appealing from a theoretical standpoint, for the simplicity in design and implementation in practice they are normally excluded from the finite optimal control problem.
### Method 6 (Aguiar & Hespanha, 2007)
[[## Methods Overview]]
**Controlled variables**: $u,r, \ddot{\gamma}$
**Type**: Body frame

For body frame the control dynamics system control law for $\boldsymbol{\mathrm{u}}=[u,r]$ and $\ddot{\gamma}$ is follows
$$
\begin{matrix*}[l]
\boldsymbol{\mathrm{u}}=\bar{\Delta}\left(R^\mathcal{B}_\mathcal{I}(\psi)\boldsymbol{p}'_d(\gamma)\mathrm{v}_d-K_p\boldsymbol{e}_\mathcal{B} \right)\\
\ddot{\gamma}=-k_\gamma e_\gamma+\boldsymbol{e}^\intercal_\mathcal{B}R^\mathcal{B}_\mathcal{I}(\psi)\boldsymbol{p}'_d(\gamma)+\ddot{\mathrm{v}}_d
\end{matrix*}
$$
render the origin of $\mathrm{\boldsymbol{x}}$ GES (Global Exponential Stability), where $\bar{\Delta}=\Delta^\intercal(\Delta\Delta^\intercal)^{-1}$ , $K_p$ is a positive definite matrix with appropriate dimension, and $k_\gamma>0$.

```pseudo
    \begin{algorithm}
    \caption{Method 6}
	    \begin{algorithmic}
		    \State Initialize $\gamma(0), \dot{\gamma(0)}$
		    \State For every sampling interval:
			\Procedure{PFController}{}
				\State Compute the position errors $\boldsymbol{e}_\mathcal{B}$ and tracking the error $e_\gamma$
				\State For inner‐loop controllers:
				\State - Compute the desired vehicle's forward speed  and yaw rate $\boldsymbol{\mathrm{u}}$
				\State - Compute the desired vehicle's yaw $\psi$
				\State Compute $\ddot{\gamma}$, integrate, and update $\gamma$
			\EndProcedure
	    \end{algorithmic}
    \end{algorithm}
```
**Notes**:
* We can control the evolution of the "reference point" by assigning $\dot{\gamma}=v_d$ instead of using the control law for $\ddot\gamma{}$. However, it  implies that the “reference point” moves without taking into consideration the state of the vehicle.

### Method 7 (Hung et al., 2020, NMPC)
[[## Methods Overview]]
**Controlled variables**: $u,r, \dot{\gamma}$
**Type**: Body frame

The state $\boldsymbol{\mathrm{x}}_\mathcal{B}$ and input $\boldsymbol{\mathrm{u}}_\mathcal{B}$ of the complete path following system are defined as follows:
$$
\begin{matrix*}[l]
\boldsymbol{\mathrm{x}}_\mathcal{B} \triangleq \left[ \boldsymbol{e}^\intercal_\mathcal{B}, \psi,\gamma \right]^\intercal \in \mathbb{R}^4 \\
\boldsymbol{\mathrm{u}}_\mathcal{B} \triangleq [u,r,v_\gamma]^\intercal \in \mathbb{R}^3
\end{matrix*}
$$
The dynamics of the complete path following state can be obtained as
$$
\dot{\boldsymbol{\mathrm{x}}}_\mathcal{B} =
\boldsymbol{\mathrm{f_\mathcal{B}}}(\boldsymbol{\mathrm{x}}_\mathcal{B}, \boldsymbol{\mathrm{u}}_\mathcal{B})
\triangleq
\begin{bmatrix}
-S(\boldsymbol{w})\boldsymbol{e}_\mathcal{B} + \Delta \boldsymbol{u} - R^{\mathcal{B}}_{\mathcal{I}}(\psi)\boldsymbol{p}'_d(\gamma)v_\gamma \\
r \\
v_\gamma
\end{bmatrix}
$$The objective of the NMPC scheme is to find an optimal control strategy for $\boldsymbol{\mathrm{u}}_\mathcal{B}$ to drive the position error $\boldsymbol{e}_\mathcal{B}$ and the speed tracking error $(e_\gamma - v_d)$ to zero.
In this case a finite horizon open loop optimal control problem (FOCP-2) that the MPC solves at every sampling time as follows:
$$
\begin{matrix}
\min{J_\mathcal{B}(\boldsymbol{\mathrm{x}}_\mathcal{B},\bar{\boldsymbol{u}}_\mathcal{B}(\cdot))} \\
\textbf{subject to} \\
\dot{\boldsymbol{\mathrm{x}}}_\mathcal{B}(\tau) = \boldsymbol{\mathrm{f}}_\mathcal{B}(\bar{\boldsymbol{\mathrm{x}}}_\mathcal{B}(\tau), \bar{\boldsymbol{\mathrm{u}}}_\mathcal{B}(\tau)), \tau \in [t, t + T_p], \\
\bar{\boldsymbol{\mathrm{x}}}_\mathcal{B}(\tau) = \boldsymbol{\mathrm{x}}_\mathcal{B}(\tau), \\
\bar{\boldsymbol{\mathrm{u}}}_\mathcal{B}(\tau) \in \mathbb{U}_\mathcal{B}, \tau \in [t, t + T_p], \\
\bar{\boldsymbol{\mathrm{e}}}_\mathcal{B}(\tau) \in \mathbb{E}_\mathcal{B}, \tau \in [t, t + T_p] \\
\textbf{with} \\
\displaystyle J_\mathcal{B}(\boldsymbol{\mathrm{x}}_\mathcal{B},\bar{\boldsymbol{u}}_\mathcal{B}(\cdot))
\triangleq
\int^{t+T_p}_{t}
\left\lVert
\bar{\boldsymbol{e}}_\mathcal{B}(\tau)
\right\lVert_Q
+
\left\lVert
\bar{\boldsymbol{u}}_b(\tau)
\right\lVert_R
+
\left\lVert
v_\gamma(\tau) - v_d(\tau)
\right\lVert_O d\tau
+
F_\mathcal{B}(\bar{\boldsymbol{e}}_\mathcal{B}(t+T_p))
\end{matrix}
$$
where:
* $Q, R, O$  are positive definite matrices,
* $\boldsymbol{u}_b$ is the cost associated with the input that is defined as
*$$
\boldsymbol{u}_b = \Delta\boldsymbol{u}-R^{\mathcal{B}}_{\mathcal{I}}(\psi)\boldsymbol{p}'_d(\gamma)v_\gamma
$$In the MPC scheme, the FOCP‐2 is repeatedly solved at every discrete sampling instant $t_i=iT_s, i \in \mathbb{N}_+$ where $T_s$ is sampling interval. Let $\bar{\mathrm{\boldsymbol{u}}}^*_\mathcal{B}, \tau \in [t, t + T_p]$ be the optimal solution of the FOCP-1. Then the **MPC control law** $\boldsymbol{u}_\mathcal{B}(\cdot)$ is defined by
$$
\boldsymbol{u}_\mathcal{B}(t) = \bar{\mathrm{\boldsymbol{u}}}^*_\mathcal{B}, \tau \in [t_i, t_i + T_s]
$$
```pseudo
    \begin{algorithm}
    \caption{Method 7}
	    \begin{algorithmic}
		    \State Initialize $\gamma(0)$
		    \State For every time $t$ do:
			\Procedure{PFController}{}
				\State Compute the position errors $s_1, y_1, \psi_e$
				\State Solve the FOCP‐2 and apply the NMPC control law to obtain optimal values of $u, r, v_\gamma$
				\State For inner‐loop controllers:
				\State - the optimal $u$ is used as the desired vehicle's forward speed.
				\State - the optimal $r$ is used as the desired vehicle's heading rate.
				\State Iterate $\gamma$ with the optimal input $v_\gamma$ to update $\gamma$
			\EndProcedure
	    \end{algorithmic}
    \end{algorithm}
```
**Notes**:
* For simplicity of design and implementation we can exclude the terminal constraints above from the finite optimal control problem.