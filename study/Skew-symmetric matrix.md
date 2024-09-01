---
date: 2024-09-01
tags:
  - theory
  - Matrix
  - SkewSymmetric
---
[[Handbook of Marine Craft Hydrodynamics and Motion Control]], Chapter 2.2

A matrix $\boldsymbol{S} \in SS(n)$, that is the set of skew-symmetric matrices of order $n$, is said to be skew-
symmetrical if
$$
\boldsymbol{S} = -\boldsymbol{S}^\intercal
$$

This implies that the off-diagonal elements of $\boldsymbol{S}$ S satisfy $s_{ij}=-sP_{ji}$ for $i \neq j$  while the diagonal elements
are zero.

The vector cross-product $\times$ is defined by
$$
\boldsymbol{\lambda} \times \boldsymbol{a} = \boldsymbol{S}(\boldsymbol{\lambda}) \boldsymbol{a}
$$
where $\boldsymbol{S} \in SS(3)$ is defined as 
$$
\boldsymbol{S}(\boldsymbol{\lambda}) = -\boldsymbol{S}^\intercal(\boldsymbol{\lambda}) = 
\begin{bmatrix}
0 & -\lambda_3 & \lambda_2 \\
\lambda_3 & 0 & -\lambda_1 \\
-\lambda_2 & \lambda_1 & 0 \\
\end{bmatrix},
\boldsymbol{\lambda} =
\begin{bmatrix}
\lambda_1 \\
\lambda_2 \\
\lambda_3
\end{bmatrix}
$$

For case $\boldsymbol{S} \in SS(2)$:
$$
\boldsymbol{S}(\boldsymbol{\lambda}) = -\boldsymbol{S}^\intercal(\boldsymbol{\lambda}) = 
\begin{bmatrix}
0 & -\lambda_1 \\
\lambda_1 & 0 \\
\end{bmatrix},
\boldsymbol{\lambda} =
\begin{bmatrix}
\lambda_1 \\
0
\end{bmatrix}
$$