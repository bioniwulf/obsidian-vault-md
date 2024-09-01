---
date: 2024-08-25
tags:
  - theory
  - Frenet-Serret
aliases:
  - Frenet–Serret frame
  - F-S frame
---
In [differential geometry](https://en.wikipedia.org/wiki/Differential_geometry "Differential geometry"), the **Frenet–Serret formulas** describe the [kinematic](https://en.wikipedia.org/wiki/Kinematic "Kinematic") properties of a particle moving along a differentiable [curve](https://en.wikipedia.org/wiki/Curve "Curve") in three-dimensional [Euclidean space](https://en.wikipedia.org/wiki/Euclidean_space "Euclidean space") $\mathbb{R}^3$, or the geometric properties of the curve itself irrespective of any motion. More specifically, the formulas describe the [derivatives](https://en.wikipedia.org/wiki/Derivative "Derivative") of the so-called **tangent, normal, and binormal** [unit vectors](https://en.wikipedia.org/wiki/Unit_vector "Unit vector") in terms of each other ([Wiki](https://en.wikipedia.org/wiki/Frenet%E2%80%93Serret_formulas)).
## Description (2D case)

![[Pasted image 20240825110159.png]]

Let $\mathcal{P}$ be a spatial path defined in an inertial frame and parameterised by a scalar variable $\gamma$ (e.g., arc‐length of the path). Normally, $\gamma \in \Omega := [a, b]$ where $a, b \in \mathbb{R}$ are values of $\gamma$ corresponding to the points at beginning and end of the path. 
If the position of a generic point $P$ on the path in the inertial frame $\{\mathcal{I}\}$ is described by vector
$$
\boldsymbol{p}_d(\gamma)=[x_d(\gamma), y_d(\gamma)]^\intercal
$$
Then:
$$
\boldsymbol{t}(\gamma) = \frac{\boldsymbol p'_d(\gamma)}{\|\boldsymbol p'_d(\gamma\|}, \boldsymbol{n}(\gamma) = \frac{\boldsymbol t'(\gamma)}{\|\boldsymbol t'(\gamma\|}
$$
be the basis vectors defining the **F‐S** frame at the point $p_d(\gamma)$ where, for every differentiable $\boldsymbol{f}'(x)$, $\boldsymbol{f}'(x) \triangleq \partial{\boldsymbol{f}(x)} / \partial{x}$. These vectors define the **tangent** and  **normal** unit normal vectors respectively to the path at the point determined by $\gamma$. The curvature $k(\gamma)$ of the path at that point is given by
$$
k(\gamma)=\|\boldsymbol t'(\gamma\|
$$
## Literature
* The F‐S frame is used in the path following methods described in Kaminer et al. ([2012](https://www.sciencedirect.com/science/article/pii/S1474667016415715)); Lapierre et al. ([2003](https://ieeexplore.ieee.org/stamp/stamp.jsp?arnumber=1272781)).
* A detailed description of this frame for 3D curves can be found in Gray et al. ([2006](https://www.routledge.com/Modern-Differential-Geometry-of-Curves-and-Surfaces-with-Mathematica/Abbena-Salamon-Gray/p/book/9781584884484?srsltid=AfmBOor4BDYI5r6XZd_opWnhz7EWXN9pIDxwUt0msJ2TvjAJTXJ6Fz1K)).
## External resources
[* Understanding the Frenet-Serret frame](https://sakshik.medium.com/understanding-the-frenet-serret-frame-3b9c730e8b1c)
## Notes
* **F‐S** frame is not well‐defined for paths that have a vanishing second derivative (i.e., zero curvature) such as straight lines or non-convex curves. The other alternative frame, called [[Parallel Transport frame]], overcomes this limitation and is presented next.
* Intuitively, curvature measures the failure of a curve to be a straight line, while torsion measures the failure of a curve to be planar ([Wiki](https://en.wikipedia.org/wiki/Frenet%E2%80%93Serret_formulas)).
* Since $\boldsymbol{t}(\gamma)$ always has unit, that $\boldsymbol{n}(\gamma)$ (the change of $\boldsymbol{t}(\gamma)$) is always perpendicular to $\boldsymbol{t}(\gamma)$, since there is no change in length of $\boldsymbol{t}(\gamma)$. Note that by calling curvature we automatically obtain the first relation.
* From a path following formulation standpoint, with the F‐S frame, the path following error is not well‐defined at inflection points because the cross‐track error (the position error projected on the normal vector) switches sign, which is not the case with the [[Parallel Transport frame]] frame.