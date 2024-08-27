---
date: 2024-08-25
tags:
  - details
aliases:
  - Parallel Transport frame, P-T frame
---
## History 
This frame was introduced in Hanson and Ma (1995) and used for the first time in the path following method of Kaminer et al. (2010). The **P‐T** frame is based on the observation that, while the tangent vector for a given curve is unique, we may choose any convenient arbitrary normal vector so as to make it perpendicular to the tangent and vary smoothly throughout the path regardless of the curvature (Hanson & Ma, 1995).
## Description (2D case)
![[Pasted image 20240825110159.png]]
In 2D, a simple way to define the **P‐T** frame is as follows. Let $\mathcal{P}$ be a spatial path defined in an inertial frame and parameterised by a scalar variable $\gamma$ (e.g., arc‐length of the path). Normally, $\gamma \in \Omega := [a, b]$ where $a, b \in \mathbb{R}$ are values of $\gamma$ corresponding to the points at beginning and end of the path. 
If the position of a generic point $P$ on the path in the inertial frame $\{\mathcal{I}\}$ is described by vector
$$
\boldsymbol{p}_d(\gamma)=[x_d(\gamma), y_d(\gamma)]^\intercal
$$
Then $\boldsymbol{t}(\gamma)$ can be denoted as:
$$
\boldsymbol{t}(\gamma) = \frac{\boldsymbol p'_d(\gamma)}{\|\boldsymbol p'_d(\gamma\|}
$$
The second basic vector, called normal vector $\boldsymbol{n}_1({\gamma})$, is obtained by rotating the tangent vector $\boldsymbol{t}(\gamma)$ 90 degree clockwise. This, as shown in Breivik and Fossen (2005), is equivalent to translating $\{\mathcal{I}\}$  to the "reference point" $P$ and then rotating it about the z‐axis by the angle:
$$
\psi_{\mathcal{P}} = \arctan \left( \frac{y'_d(\gamma)}{x'_d(\gamma)} \right)
$$
## Notes
* tangent basic vector in **P‐T** frame is the same as in [[Frenet–Serret frame]], but normal vector is obtained by rotating the tangent vector 90 clockwise.
* Another way of propagating a **P‐T** frame along the path is to use the algorithm proposed in Hanson and Ma ([1995](https://legacy.cs.indiana.edu/ftp/techreports/TR425.pdf)). While this algorithm is general and efficient for 3D, it is unnecessarily complicated for 2D curves.