---
date: 2024-09-10
title: Vehicle Dynamics
tags:
  - theory
  - DynamicSystems
notation: "[[SNAME Notation]]"
---

Consider the nonlinear equations of motion expressed in $\{b\}$ with $\boldsymbol{\nu}_c= \boldsymbol{0}$:
## Nonlinear 6 DOF Vector Representations in BODY and NED
The kinematics of an underwater vehicle can be represented in the following way ([[Vehicle Kinematics]]):
$$
\dot{\boldsymbol{\eta}} = \boldsymbol{J}_{k}(\boldsymbol{\eta})\boldsymbol{\nu}
$$
$$
\begin{matrix}
\dot{\boldsymbol{\eta}} = \boldsymbol{J}_{k}(\boldsymbol{\eta})\boldsymbol{\nu} \\
\boldsymbol{M}\dot{\boldsymbol{\nu}} + \boldsymbol{C}(\boldsymbol{\nu})\boldsymbol{\nu} + \boldsymbol{D}(\boldsymbol{\nu})\boldsymbol{\nu} + \boldsymbol{g}(\boldsymbol{\eta})=\boldsymbol{\tau}
\end{matrix}
$$
where
$$
\begin{matrix*}[l]
\boldsymbol{M} = \boldsymbol{M}_{RB} + \boldsymbol{M}_A \\
\boldsymbol{C}(\boldsymbol{\nu}) = \boldsymbol{C}_{RB}(\boldsymbol{\nu}) + \boldsymbol{C}_{A}(\boldsymbol{\nu}) \\
\boldsymbol{D}(\boldsymbol{\nu}) = \boldsymbol{D} + \boldsymbol{D}_n(\boldsymbol{\nu})
\end{matrix*}
$$
[[Handbook of Marine Craft Hydrodynamics and Motion Control]], Chapter 6.0.0
The dynamics of and underwater vehicle be represented as follows
$$
\underbrace{
	\boldsymbol{M}_{RB}\dot{\boldsymbol{\nu}} +
	\boldsymbol{C}_{RB}(\boldsymbol{\nu})\nu
}_{\text{rigid-body forces}}
+
\underbrace{
	\boldsymbol{M}_{A}\dot{\boldsymbol{\nu}}_r +
	\boldsymbol{C}_{RB}(\boldsymbol{\nu}_r)\boldsymbol{\nu}_r +
	\boldsymbol{D}(\boldsymbol{\nu}_r)\boldsymbol{\nu}_r
}_{\text{hydrodynamic force}}
+
\underbrace{
	\boldsymbol{g}(\boldsymbol{\eta})+
	\boldsymbol{g}_0
}_{\text{hydrostatic force}}
=
\boldsymbol{\tau} + \boldsymbol{\tau}_{\text{wind}}+\boldsymbol{\tau}_{\text{wave}}
$$
where:
* $\boldsymbol{M} = \boldsymbol{M}_{RB} + \boldsymbol{M}_A$ - system inertia matrix (including added mass)
* $\boldsymbol{C}(\boldsymbol{\nu}) = \boldsymbol{C}_{RB}(\boldsymbol{\nu}) + \boldsymbol{C}_{A}(\boldsymbol{\nu})$ - Coriolis–centripetal matrix (including added mass)
* $\boldsymbol{D}(\boldsymbol{\nu}_r)$ - damping matrix
* $\boldsymbol{g}(\boldsymbol{\eta})$ - vector of gravitational/buoyancy forces and moments
* $\boldsymbol{g}_0$ - vector used for pretrimming (ballast control)
* $\boldsymbol{\tau}$ - vector of control inputs
* $\boldsymbol{\tau}_{\text{wind}}$ - vector of wind forces
* $\boldsymbol{\tau}_{\text{wave}}$ - vector of wave-induced forces
The expressions for $\boldsymbol{\eta}$ and $\boldsymbol{J}_{k}(\boldsymbol{\eta})$ depend on the kinematic representation. Three different choices for $\boldsymbol{J}_{k}(\boldsymbol{\eta})$ will be presented where the subscript $k \in \{\Theta, q, r\}$ denotes the **Euler angle**, **quaternion** and **rotation matrix** representation, respectively.
The vector $\boldsymbol{\nu}_r = \boldsymbol{\nu} - \boldsymbol{\nu}_c$ where $\boldsymbol{\nu}_c = [u,v,w,0,0,0]^\intercal$ is an ocean current vector.
### Inertia Matrix $\boldsymbol{M}$
$$
\begin{matrix*}[l]
\boldsymbol{M} = \boldsymbol{M}_{RB} + \boldsymbol{M}_A
\end{matrix*}
$$
Where $\boldsymbol{M}_{RB}$ is rigid-body inertia matrix and the $\boldsymbol{M}_A$ addition relates to added mass of water.
[[Handbook of Marine Craft Hydrodynamics and Motion Control]], Chapter 3.3.1
$$
\boldsymbol{M}_{RB} =
\begin{bmatrix}
m\boldsymbol{I}_{3 \times 3} & -m\boldsymbol{S}(\boldsymbol{r}_g^b) \\
m\boldsymbol{S}(\boldsymbol{r}_g^b) & \boldsymbol{I}_b
\end{bmatrix} =
\begin{bmatrix}
	m & 0 & 0 & 0 & m z_g  & -m y_g \\
    0 & m & 0 & -m z_g & 0 & m x_g \\
    0 & 0 & m & m y_g & -m x_g & 0 \\
    0 & -m z_g & m y_g & J_{x} & -J_{xy} & -J_{xz} \\
    m z_g & 0 & -m x_g & -J_{yx} & J_{y} & -J_{yz} \\
    -m y_g & m x_g & 0 & -J_{zx} & -J_{zy} & J_{z}
\end{bmatrix}
$$
Where $\boldsymbol{S}$ is [[Skew-symmetric matrix]] and $\boldsymbol{I}_b$ is the inertia matrix.
If Origin **CO** coincides with the **CG**. That implies that $\boldsymbol{r}_g^b=[0,0,0]^\intercal$, $\boldsymbol{I}_b=\boldsymbol{I}_g$, then
$$
\boldsymbol{M}_{RB} =
\begin{bmatrix}
m\boldsymbol{I}_{3\times3} & \boldsymbol{0}_{3\times3} \\
\boldsymbol{0}_{3\times3} & \boldsymbol{I}_g
\end{bmatrix}
$$
[[Handbook of Marine Craft Hydrodynamics and Motion Control]], Chapter 6.3.3
In general, the motion of an underwater vehicle moving in 6 DOF at high speed will be highly nonlinear and coupled. However, in many AUV and ROV applications the vehicle will only be allowed to move at low speed. If the vehicle also has three planes of symmetry, this suggests that the contribution from the **off-diagonal elements** in the matrix $\boldsymbol{M}_A$ **can be neglected**. Hence, the following simple expressions for the matrix $\boldsymbol{M}_A$ is obtained:
$$
\boldsymbol{M}_A = \boldsymbol{M}_A^{\intercal} = -\text{diag}\{X_\dot{u},Y_\dot{v}, Z_\dot{w}, K_\dot{p}, M_\dot{q},N_\dot{r} \}
$$
*The diagonal structure is often used since it is time consuming to determine the off-diagonal elements from experiments as well as theory. In practice, the diagonal approximation is found to be quite good for many applications. This is due to the fact that the off-diagonal elements of a positive inertia matrix will be much smaller than their diagonal counterparts.*
## Restoring vector $\boldsymbol{g}(\boldsymbol{\eta})$
[[Handbook of Marine Craft Hydrodynamics and Motion Control]], Chapter 4.1.1

$$
\boldsymbol{g}(\boldsymbol{\eta}) = -
    \begin{bmatrix}
        \boldsymbol{R}^n_b(\boldsymbol{\Theta}_{nb})^{-1}(\boldsymbol{f}_g^n + \boldsymbol{f}_b^n) \\
        \boldsymbol{r}_g^b \times \boldsymbol{R}^n_b(\boldsymbol{\Theta}_{nb})^{-1} \boldsymbol{f}_g^n + \boldsymbol{r}_b^b \times \boldsymbol{R}^n_b(\boldsymbol{\Theta}_{nb})^{-1} \boldsymbol{f}_b^n
    \end{bmatrix} =
$$
$$
=
\begin{bmatrix}
	(W - B)\sin{\theta} \\
	-(W - B)\cos{\theta} \sin{\phi} \\
	-(W - B)\cos{\theta} \cos{\phi} \\
	-(y_gW - y_bB)\cos{\theta} \cos{\phi} + (z_gW - z_bB)\cos{\theta} \sin{\phi} \\
	(z_gW - z_bB)\sin(\theta) + (x_gW - x_bB)\cos{\theta} \cos{\phi} \\
	-(x_gW - x_bB)\cos{\theta} \sin{\phi} - (y_gW - y_bB) \sin{\theta}
\end{bmatrix}
$$
Let's assume that **CG** and **CB** are located vertically on the $z$ axis ( $x_b=x_g=0$ and $y_b=y_g=0$) and reference point located in the **CG** ($z_g=0$), $H_m =-z_b$ is the metacentric height and $B_r = (B-W)>0$ is the residual buoyancy.
This yields to
$$
\boldsymbol{g}(\boldsymbol{\eta}) =
\begin{bmatrix}
-B_r\sin{\theta} \\
B_r\cos{\theta} \sin{\phi} \\
B_r\cos{\theta} \cos{\phi} \\
H_mB\cos{\theta} \sin{\phi} \\
H_mB\sin{\theta} \\
0
\end{bmatrix}
$$
## Coriolis–Centripetal Matrix $\boldsymbol{C}(\boldsymbol{\nu})$
The nonlinear Coriolis and centripetal matrix $\boldsymbol{C}(\boldsymbol{\nu})$ arises due to a rotation of $\{b\}$ about the inertial frame $\{n\}$.
$$\boldsymbol{C}(\boldsymbol{\nu}) = \boldsymbol{C}_{RB}(\boldsymbol{\nu}) + \boldsymbol{C}_{A}(\boldsymbol{\nu})$$
[[Handbook of Marine Craft Hydrodynamics and Motion Control]], Chapter 6.3.1
The matrix $\boldsymbol{C}_{RB}(\boldsymbol{\nu})$ in represents the Coriolis vector term $\boldsymbol{\omega}_{b/n}^b \times \boldsymbol{v}_{b/n}^b$ and the centripetal vector term $\boldsymbol{\omega}_{b/n}^b \times (\boldsymbol{\omega}_{b/n}^b \times \boldsymbol{r}_g^b)$.
Using velocity-independent parametrizations, the matrix could be written as 
$$
\boldsymbol{C}_{RB}(\boldsymbol{\nu}) = 
\begin{bmatrix}
m\boldsymbol{S}(\boldsymbol{\nu_2}) & -m\boldsymbol{S}(\boldsymbol{\nu_2})\boldsymbol{S}(\boldsymbol{r_g^b}) \\
m\boldsymbol{S}(\boldsymbol{\nu_2})\boldsymbol{S}(\boldsymbol{r_g^b}) & -\boldsymbol{
S}(\boldsymbol{I}_b\boldsymbol{\nu}_2)
\end{bmatrix}
$$
where $\boldsymbol{\nu}_2=\boldsymbol{\omega}_{b/n}^b=[p,q,r]^\intercal$, $\boldsymbol{S}$ is [[Skew-symmetric matrix]] and $\boldsymbol{I}_b$ is the inertia matrix.
Assume that $\boldsymbol{I}_b$ is diagonal (**CO** located in center of symmetry), then $\boldsymbol{C}_{RB}(\boldsymbol{\nu})$ can be significantly simplified
$$
\boldsymbol{C}_{RB}(\boldsymbol{\nu})=
\begin{bmatrix}
0 & 0 & 0 & 0 & mw & -mv \\
0 & 0 & 0 & -mw & 0 & mu \\
0 & 0 & 0 & mv & -mu & 0 \\
0 & mw & -mv & 0 & I_zr & -I_yq \\
-mw & 0 & mu & -I_zr & 0 & I_xp \\
mv & -mu & 0 & I_yq & -I_xp & 0
\end{bmatrix}
$$

[[Handbook of Marine Craft Hydrodynamics and Motion Control]], Chapter 6.3.2
For a rigid body moving through an ideal fluid the hydrodynamic Coriolis and centripetal matrix $\boldsymbol{C}_{A}(\boldsymbol{\nu})$ can always be parameterized such that it is skew-symmetric $\boldsymbol{C}_{A}(\boldsymbol{\nu})=-\boldsymbol{C}_{A}^{\intercal}(\boldsymbol{\nu})$. Based on the expression for the fluid kinetic energy $T_A$ the $\boldsymbol{C}_{A}(\boldsymbol{\nu})$ is can be derived from $\boldsymbol{M}_A$ such as
$$
\boldsymbol{C}_{A}(\boldsymbol{\nu})=
\begin{bmatrix}
\boldsymbol{0}_{3\times3} & -\boldsymbol{S}(\boldsymbol{A}_{11}\boldsymbol{\nu}_{1} + \boldsymbol{A}_{12}\boldsymbol{\nu}_{2}) \\
-\boldsymbol{S}(\boldsymbol{A}_{11}\boldsymbol{\nu}_{1} + \boldsymbol{A}_{12}\boldsymbol{\nu}_{2})
& -\boldsymbol{S}(\boldsymbol{A}_{21}\boldsymbol{\nu}_{1} + \boldsymbol{A}_{22}\boldsymbol{\nu}_{2})
\end{bmatrix}
$$
where $\boldsymbol{A}_{ij} \in \mathbb{R}^{3\times3}$ is given by
$$
\boldsymbol{M}_A=
\begin{bmatrix}
\boldsymbol{A}_{11} & \boldsymbol{A}_{12} \\
\boldsymbol{A}_{21} & \boldsymbol{A}_{22} \\
\end{bmatrix}
$$
In case if off-diagonal elements in the matrix $\boldsymbol{M}_A$ can be neglected, the $\boldsymbol{C}_{A}(\boldsymbol{\nu})$ obtains following form
$$
\boldsymbol{C}_{A}(\boldsymbol{\nu})=-\boldsymbol{C}_{A}^\intercal(\boldsymbol{\nu})=
\begin{bmatrix}
0 & 0 & 0 & 0 & -Z_\dot{w}w_r & Y_\dot{v}v_r \\
0 & 0 & 0 & Z_\dot{w}w_r & 0 & -X_\dot{u}u_r \\
0 & 0 & 0 & -Y_\dot{v}v_r & X_\dot{u}u_r & 0 \\
0 & -Z_\dot{w}w_r & Y_\dot{v}v_r & 0 & -N_\dot{r}r & M_\dot{q}q \\
Z_\dot{w}w_r & 0 & -X_\dot{u}u_r & N_\dot{r}r & 0 & -K_\dot{p}p \\
-Y_\dot{v}v_r & X_\dot{u}u_r & 0 & -M_\dot{q}q & K_\dot{p}p & 0
\end{bmatrix}
$$
where $Y_\dot{v}$ and others are hydrodynamic derivatives in SNAME notation [[SNAME Notation]].