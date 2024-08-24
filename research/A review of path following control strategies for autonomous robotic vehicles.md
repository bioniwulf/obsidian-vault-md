---
date: 2024-08-20
tags:
  - article
title: "A review of path following control strategies for autonomous robotic vehicles: Theory, simulations, and experiments"
link: https://onlinelibrary.wiley.com/doi/full/10.1002/rob.22142
---

| Notation                                                                                              | Description                                                                                                                   |
| ----------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------- |
| $Q$                                                                                                   | vehicle centre of mass                                                                                                        |
| $\{I\} = \{x_I , y_I \}$                                                                              | inertial (global) North‐East (NE) frame                                                                                       |
| $\{B\} = \{x_b, y_b\}$                                                                                | vehicle body fixed frame with $Q$ in the centre                                                                               |
| $\{P\} = \{x_p, y_p\}$                                                                                | path frame                                                                                                                    |
| $\boldsymbol{p}_d(\gamma)=[x_d(\gamma), y_d(\gamma)]^⊤$                                               | desired path points parameterised by scalar $\gamma$ parameter (e.g., arc‐length of the path)                                 |
| $\boldsymbol{p} = [x, y]^{\intercal}$                                                                 | vehicle position in $\{I\}$                                                                                                   |
| $\psi$                                                                                                | vehicle heading in $\{I\}$                                                                                                    |
| $\boldsymbol{v} = [u, v]^{\intercal}$                                                                 | vehicle velocity in $\{B\}$                                                                                                   |
| $\boldsymbol{v_c} = [v_{cx}, v_{cy}]^{\intercal}$                                                     | external unknown disturbances (e.g., ocean current in the case of marine vehicles and wind in the case of aerial<br>vehicles) |
| $\displaystyle \psi_P = \arctan \left( \frac{y`_d(\gamma)}{x`_d(\gamma)} \right)$                     | tangent angle of the path at point $\gamma$ expressed in the $\{I\}$                                                          |
| $\boldsymbol{e}_p \triangleq [s_1, y_1]^{\intercal}$                                                  | the position error between the vehicle and the reference point P                                                              |
| $s_1, y_1$                                                                                            | along‐track and cross‐track errors, respectively                                                                              |
| $\psi_e = \psi - \psi_P$                                                                              | the orientation error between the vehicle's heading and the tangent to the path                                               |
| $k(\gamma)=\| \boldsymbol t'(\gamma) \|$                                                              | the curvature of the path                                                                                                     |
| $\displaystyle \boldsymbol{t}(\gamma) = \frac{\boldsymbol p'_d(\gamma)}{\|\boldsymbol p'_d(\gamma\|}$ | unit tangent vector respectively to the path                                                                                  |
| $\displaystyle \boldsymbol{n}(\gamma) = \frac{\boldsymbol t'(\gamma)}{\|\boldsymbol t'(\gamma\|}$     | principle unit normal respectively to the path                                                                                |
| $U_d(t)$                                                                                              | positive desired longitudinal speed of the vehicle                                                                            |
| $u_P = \dot{\boldsymbol{p_d}}= \|\boldsymbol{p}'_d(\gamma)\|\dot{\gamma}$                             | speed of reference point P with respect to the $\{I\}$                                                                        |
| $r_P=k(\gamma)u_P$                                                                                    | the angular velocity vector of $\{P\}$ respect to $\{I\}$ expressed in $\{P\}$                                                |
| $\displaystyle v_d(\gamma,t) \triangleq \frac{1}{\|\boldsymbol{p}'_d(\gamma)\|}U_d(\gamma, t)$        | desired speed profile for $\dot{\gamma}$                                                                                      |
| $\boldsymbol{R}^P_I$                                                                                  | Rotation matrix from $\{P\}$ to $\{I\}$                                                                                       |

**Notes**:
* there are two frames adopted in the literature to formulate the path following problem, that is, to describe the position error between the vehicle and the path. Namely, the [[Frenet–Serret frame]](F-S) frame ([link](https://sakshik.medium.com/understanding-the-frenet-serret-frame-3b9c730e8b1c)) and the [[Parallel Transport frame]] (P‐T) frame.
* **(F‐S)** frame is that it is not well‐defined for paths that have a vanishing second derivative (i.e., zero curvature) such as straight lines or nonconvex curves.
* tangent basic vector in **(P‐T)** is the same as in **(F‐S)**, but normal vector is obtained by rotating the tangent vector 90 clockwise.

### 1 INTRODUCTION
![[Pasted image 20240823153409.png]]
### 2 PROBLEM FORMULATION AND COMMON PRINCIPLES OF PATH FOLLOWING METHODS
##### 2.1 Vehicle kinematic models
![[Pasted image 20240823113051.png]]
Vehicle's equations of motion:
$$
\begin{matrix*}[l]
   \dot{x} = u \cos(\psi) - v\sin{\psi} + v_{cx} \\
   \dot{y} = u \sin(\psi) + v \cos{\psi} + v_{cy} \\
   \dot{\psi} = r
\end{matrix*}
$$
###### 2.1.1 Scenario 1: Under‐actuated vehicle without external disturbances
Vehicle's equations of motion:
$$
\begin{matrix*}[l]
   \dot{x} = u \cos(\psi)  \\
   \dot{y} = u \sin(\psi)  \\
   \dot{\psi} = r
\end{matrix*}
$$
###### 2.1.2 Scenario 2: Under‐actuated vehicle with external disturbances
Vehicle's equations of motion:
$$
\begin{matrix*}[l]
   \dot{x} = u \cos(\psi) + v_{cx} \\
   \dot{y} = u \sin(\psi) + v_{cy} \\
   \dot{\psi} = r
\end{matrix*}
$$
###### 2.1.3 Scenario 3: Fully or over‐actuated vehicle
Vehicle's equations of motion:
$$
\begin{matrix*}[l]
   \dot{x} = u \cos(\psi) - v\sin{\psi} \\
   \dot{y} = u \sin(\psi) + v \cos{\psi} \\
   \dot{\psi} = r
\end{matrix*}
$$
##### 2.2 Path parameterization and path frames
![[Pasted image 20240823112821.png]]
**Notes**:
* there are two frames adopted in the literature to formulate the path following problem, that is, to describe the position error between the vehicle and the path. Namely, the **Frenet–Serret (F‐S)** ([link](https://sakshik.medium.com/understanding-the-frenet-serret-frame-3b9c730e8b1c)) and the **Parallel Transport (P‐T)** frames.
###### 2.2.1 Frenet–Serret frame, Gray et al.
Unit tangent and principle unit normal respectively to the path:
$$
\boldsymbol{t}(\gamma) = \frac{\boldsymbol p'_d(\gamma)}{\|\boldsymbol p'_d(\gamma\|}, \boldsymbol{n}(\gamma) = \frac{\boldsymbol t'(\gamma)}{\|\boldsymbol t'(\gamma\|}
$$
The curvature $k(\gamma)=\|\boldsymbol t'(\gamma\|$
###### 2.2.2 Parallel–Transport frame, Hanson and Ma
##### 2.3 Path following formulation
1. **Geometric task**: steer position error $\boldsymbol{e} \triangleq \boldsymbol{p} - \boldsymbol{p_d}$, s.t.
$$
\lim_{t\rightarrow\inf}{\boldsymbol{e}(t)} = 0
$$
4. **Dynamic task**: ensure that the vehicle's forward speed tracks a positive desired speed profile: 
$$ 
\lim_{t \rightarrow \inf}{u(t) - U_d(t)} = 0
$$
or (is equivalent)
$$
\lim_{t \rightarrow \inf}{\dot{\gamma} - v_d(\gamma,t)} = 0
$$
##### 2.4 Common principles of path following methods
| Control value $u$ | Stabilizing $e$ in path frame $\{P\}$                                                                | Stabilizing $e$ in path frame ($\{B\}$)                            |
| ----------------- | ---------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------ |
| $u$, $\psi$       | Breivik and Fossen (2005), Fossen et al. (2003),<br>Maurya et al. (2009), Papoulias (1991)           |                                                                    |
| $u$, $\dot{\psi}$ | Hung et al. (2018), Lapierre et al. (2003)$^2$, Micaelli<br>and Samson (1993)$^{1}$ Yu et al. (2015) | Aguiar and Hespanha (2007)$^6$,<br>Alessandretti et al. (2013)$^7$ |
### 3 BASIC PATH FOLLOWING METHODS
##### 3.1 Methods based on stabilizing the path following error in the path frame
The common principle behind these methods can be summarized in two steps:
	**Step 1.** Derive the dynamics of the path following error between the vehicle and the path in a path frame (e.g., F‐S or P‐T frame)
	**Step 2**. Drive these errors to zero using nonlinear control techniques to achieve path following, that is, make the vehicle converge to and move along the path with a desired speed profile.
##### 3.2 Derivation of the path following error
The position error between the vehicle and the reference point P could be rewritten in $\{I\}$ frame such as:
$$
\boldsymbol{e}_P = \boldsymbol{R}^P_I(\psi_P)(\boldsymbol{p}-\boldsymbol{p_d})
$$
The dynamics of the position error in $\{P\}$ as well as dynamics of the error orientation could be rewritten as follows:
$$
\begin{matrix*}[l]
\dot{\boldsymbol{e}}_P = -\boldsymbol{S}(\boldsymbol{w_p})\boldsymbol{e}_P +
\begin{bmatrix}
u\cos{\psi_e} \\
u\sin{\psi_e}
\end{bmatrix}
-
\begin{bmatrix}
u_P \\
0
\end{bmatrix} \\
\dot{\psi}_e = r - k(\gamma) u_P
\end{matrix*}
$$
where $\boldsymbol{S}(\boldsymbol{w_p})$ is skew  symmetric matrix parameterized by $\boldsymbol{w}_P=[r_P,0]$:
$$
\boldsymbol{S}(\boldsymbol{w_p})=
\begin{bmatrix}
0 & -r_P \\
r_P & 0
\end{bmatrix}
$$
where $r_P$ is the angular velocity vector of $\{P\}$ respect to $\{I\}$ expressed in $\{P\}$.
$r_P$ satisfies the relation:
$$
r_P = k(\gamma)u_p
$$
**Methods proposed to stabilize $\boldsymbol{e}_P$ to zero**

| PF methods | Drive $\boldsymbol{e}_P$ to zero by | References                           |
| ---------- | ----------------------------------- | ------------------------------------ |
| Method 1   | $u,r$                               | Micaelli and Samson (1993)           |
| Method 2   | $u,r, \dot{\gamma}$                 | Lapierre et al. (2003)               |
| Method 3   | $u,\psi$                            | Fossen et al. (2003, 2015)           |
| Method 4   | $u,\psi, \dot{\gamma}$              | Breivik and Fossen (2005)            |
| Method 5   | $u,r, \dot{\gamma}$                 | Hung et al. (2020), Yu et al. (2015) |
###### 3.2.1 Method 1 (Micaelli & Samson, 1993): Achieve path following by controlling ($u,r$)
In this method, the “reference point” is chosen as the orthogonal projection of the real vehicle on the path, that is, the point on the path closest to the vehicle (if it is well‐defined). With this strategy the along‐track error is always zero, that is, $s_1(t)=0$.
In this case, the dynamics of the cross‐track error can be written explicitly as:
$$
\begin{matrix*}[l]
\dot{y_1}= -r_Ps_1+u\sin{\psi_e}=u\sin{\psi_e}\\
\dot{\tilde{\psi}} = r - k(\gamma)u_P - \dot{\delta}
\end{matrix*}
$$
where $\delta(y_1,u)$  is a time differentiable design function that can be used to shape the manner in which the vehicle approaches the path, and $\delta(y_1,u) = \psi_e - \tilde{\psi}$
**So,  $u, r$ can be calculated as follows**:
$$
\begin{matrix*}[l]
u=U_d \\
r = k(\gamma)u_P+\dot{\delta}-k_1\tilde{\psi} - k_2y_1u\frac{\sin{\psi_e} - \sin{\delta}}{\tilde{\psi}}
\end{matrix*}
$$
where $k1_, k_2$ are tuning parameters.
The function $\delta(y_1,u)$ can be chosen as follows:
$$
\delta(y_1,u) = -\theta \tanh(k_{\delta}y_1u)
$$
where $\theta \in (0, \pi/2), k_{\delta}>0$
**Notes**:
* Because the “reference point” on the path for the vehicle to track is chosen closest to the vehicle, there exists a singularity when $y_1= 1 / k(\gamma)$
###### 3.2.2 Method 2 (Lapierre et al., 2003): Achieve path following by controlling ($u,r, \dot{\gamma}$)
**Notes**:
* To eliminate the cross‐track and orientation errors, this method uses the same controller for $u,r$ as in Method 1.
* Compared with Method 1 this strategy has the following advantages: (i) it doesn't require an algorithm to find a point on the path that is closest to the vehicle and (ii) it avoids the singularity that occurs in the Method 1.
###### 3.2.3 Method 3 (Fossen et al., 2015): LOS path following
###### 3.2.4 Method 4 (Breivik & Fossen, 2005): Achieve path following by controlling ($u,\psi, \dot{\gamma}$)
###### 3.2.5 Method 5 (Hung et al., 2020; Yu et al., 2015): NMPC‐based path following
##### 3.3 Methods based on stabilizing the path following error in the body frame
###### 3.3.1 Method 6 (Aguiar & Hespanha, 2007): Achieve path following by controlling ($u,\psi, \ddot{\gamma}$)
###### 3.3.2 Method 7 (Alessandretti et al., 2013): NMPC‐based path following
### 4 PATH FOLLOWING METHODS IN THE PRESENCE OF EXTERNAL DISTURBANCES
##### 4.1 Path following with integral terms
##### 4.2 Path following with estimation of external disturbances
###### 4.2.1 Disturbance estimation
###### 4.2.2 Method 3 with estimation of external disturbances
###### 4.2.3 Method 6 with estimation of the external disturbances
### 5 PATH ‐FOLLOWING OF FULLY AND OVER‐ACTUATED VEHICLES WITH ARBITRARY HEADING
### 6 MATLAB SIMULATION TOOLBOX AND ROS/GAZEBO IMPLEMENTATION
##### 6.1 Matlab path following toolbox
##### 6.2 Gazebo/ROS packages
### 7 SIMULATIONS AND EXPERIMENTAL RESULTS
##### 7.1 Test set‐up
##### 7.2 Simulation results with the ROS/Gazebo workpackages
###### 7.2.1 Results with an under‐actuated vehicle
###### 7.2.2 Results with an over‐actuated vehicle
##### 7.3 Experimental results
###### 7.3.1 Results with an under‐actuated vehicle
###### 7.3.2 Results with an over‐actuated vehicle
### 8 DISCUSSIONS
##### 8.1 Advantages and disadvantages of the different path following methods
##### 8.2 Other issues
### 9 CONCLUSIONS
