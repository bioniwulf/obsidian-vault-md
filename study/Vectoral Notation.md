---
date: 2024-09-01
tags:
  - theory
  - notation
  - vector
---
# 6DOF Vectoral Notation

[[Handbook of Marine Craft Hydrodynamics and Motion Control]], Chapter 2.1

We will use the notation $\vec{u}$ to refer to a **coordinate free** vector, that is a **directed line segment**. When a
vector is described relative to a coordinate system $\{n\}$, the following notation will be used:
$$
\vec{u} = u_1^n\vec{n}_1 + u_2^n\vec{n}_2 + u_2^n\vec{n}_2
$$
where $\vec{n}_i(i=1,2,3)$ are the unit vectors that define $\{n\}$, $u_i^n$ are the measures of $\vec{u}$ along $\vec{u}_i$ and $u_i^n$ are the components of  $\vec{u}$ in $\{n\}$. The coordinate form $\boldsymbol{u}_n$ which is represented by a **column vector** in $\mathbb{R}^3$ :
$$
\boldsymbol{u}_n = [u_1^n, u_2^n, u_2^n]^\intercal
$$For marine craft the following notation will be adopted for vectors in the coordinate systems $\{b\}$, $\{e\}$
and $\{n\}$:
* $\boldsymbol{v}^e_{b/n}$ - linear velocity of the point $O_b$ with respect to $\{n\}$ expressed in $\{e\}$
* $\boldsymbol{w}^b_{n/e}$ - angular velocity of $\{n\}$ with respect to $\{e\}$ expressed in $\{b\}$
* $\boldsymbol{f}^n_b$ - force with line of action through the point $O_b$ expressed in $\{n\}$
* $\boldsymbol{m}^n_b$ - moment about the point $O_b$ expressed in $\{n\}$

The [[SNAME Notation]] can be conveniently expressed in a vectorial setting according to:
**ECEF position**
$$
\boldsymbol{p}^e_{b/e} = 
\begin{bmatrix}
x \\
y \\
z
\end{bmatrix}
\in \mathbb{R}^3
$$
**NED Position**
$$
\boldsymbol{p}^n_{b/n} = 
\begin{bmatrix}
N \\
E \\
D
\end{bmatrix}
\in \mathbb{R}^3
$$
**Body-fixed linear velocity**
$$
\boldsymbol{v}^b_{b/n}
=
\begin{bmatrix}
u \\
v \\
w
\end{bmatrix}
\in \mathbb{R}^3
$$
**Body-fixed angular velocity**
$$
\boldsymbol{\omega}^b_{b/n}
=
\begin{bmatrix}
p \\
q \\
r
\end{bmatrix}
\in \mathbb{R}^3
$$
**Body-fixed force**
$$
\boldsymbol{f}^b_{b}
=
\begin{bmatrix}
X \\
Y \\
Z
\end{bmatrix}
\in \mathbb{R}^3
$$
**Body-fixed moment**
$$
\boldsymbol{m}^b_{b}
=
\begin{bmatrix}
K \\
M \\
N
\end{bmatrix}
\in \mathbb{R}^3
$$
**Longitude and latitude**
$$
\boldsymbol{\Theta}_{en}
=
\begin{bmatrix}
l \\
\mu
\end{bmatrix}
\in \mathcal{S}^2
$$
**Attitude**
$$
\boldsymbol{\Theta}_{nb}
=
\begin{bmatrix}
\phi \\
\theta \\
\psi
\end{bmatrix}
\in \mathcal{S}^3
$$
where $\mathbb{R}^3$ is the Euclidean space of dimension three and $\mathcal{S}^2$ denotes a torus of dimension two (shape of a
donut), implying that there are two angles defined on the interval $[0, 2\pi]$. In the three-dimensional (3-D)
case the set $\mathcal{S}^3$ is a sphere.

The general motion of a marine craft in **6 DOF** with $O_b$ as coordinate origin is described by the following vectors:
$$
\boldsymbol{\eta} = 
\begin{bmatrix}
\boldsymbol{p}^n_{b/n} \\
\boldsymbol{\Theta}_{nb}
\end{bmatrix},
\boldsymbol{\nu} =
\begin{bmatrix}
\boldsymbol{v}^b_{b/n} \\
\boldsymbol{\omega}^b_{b/n}
\end{bmatrix},
\boldsymbol{\tau} =
\begin{bmatrix}
\boldsymbol{f}^b_{b} \\
\boldsymbol{m}^b_{b}
\end{bmatrix}
$$
where:
* $\boldsymbol{\eta} \in \mathbb{R}^3\times \mathcal{S}^3$ denotes the position and orientation vector where the position vector $\boldsymbol{p}^n_{b/n} \in \mathbb{R}^3$ is the distance from **NED** to **BODY** expressed in **NED** coordinates,
* $\boldsymbol{\Theta}_{nb} \in \mathcal{S}^3$ is a vector of Euler angles,
* $\boldsymbol{\nu} \in \mathbb{R}^6$ is the linear and angular velocity vectors that are decomposed in the body-fixed reference frame,
* $\boldsymbol{\tau} \in \mathbb{R}^6$ is used to describe the forces and moments acting on the craft in the body-fixed frame.