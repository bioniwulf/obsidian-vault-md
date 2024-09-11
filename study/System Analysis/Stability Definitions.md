---
date: 2024-09-06
title: Stability Definitions
tags:
  - theory
  - SystemAnalysis
source: "[[EE363. Linear Dynamical Systems]]"
aliases:
---
# Stability Definitions
We consider nonlinear time-invariant system $\dot{x} = f(x)$, where $f : \mathbb{R}^n \rightarrow \mathbb{R}^n$.
A point $x_e \in \mathbb{R}^n$ is an **equilibrium point of the system** if  $f(x_e) = 0$
$x_e$ is an equilibrium point $\Longleftrightarrow$ $x(t) = x_e$ is a trajectory suppose $x_e$ is an equilibrium point.
### G.A.S.
System is globally asymptotically stable (**G.A.S.**) if for every trajectory $x(t)$, we have $x(t) \rightarrow x_e$ as $t \rightarrow \infty$ where $x_e$ is an equilibrium point.
### L.A.S.
System is locally asymptotically stable (**L.A.S.**) near or at $x_e$ if there is an $R>0$ s.t. $||x(0)-x_e|| \leq R \Rightarrow x(t) \rightarrow x_e$ as $t \rightarrow \infty$.
### G.E.S.
System is globally exponentially stable (**G.E.S.**) if for every trajectory $x(t)$ satisfies $||x(t)|| \leq Me^{-\alpha t/2}||x(0)||$
### GAS/LAS Definitions for Linear Systems
A linear system $\dot{x}=Ax$ is **G.A.S.** and **L.A.S.** (with $x_e=0$) $\Leftrightarrow$ $\mathfrak{R}\lambda_i(A) < 0$ for $i=1,\dots,n$
where $\mathfrak{R}\lambda_i(A)$ is real part of the matrix $i$-th eigenvalue.
### Energy and Dissipation Functions
Consider nonlinear system $\dot{x}=f(x)$, and function $V:\mathbb{R}^n \rightarrow \mathbb{R}$
We define $\dot{V}:\mathbb{R}^n \rightarrow \mathbb{R}$ as $\dot{V}(z)=\nabla{V}^\intercal f(z)$
We can think about of 
* $V$ as **generalized energy function**.
* $-\dot{V}$ as **generalized dissipation function**.
### Bound area
$B_r(\boldsymbol{0})$ denote the set of all points $x \in \mathbb{R}^n$ which are strictly inside a ball of radius $r$ about the origin:
$$
B_r(\boldsymbol{0}) = \{\boldsymbol{x} \in \mathbb{R}^n : \|x\| < r\}
$$
### Function definitions 
#### Positive Definite Function
a function $V:\mathbb{R}^n \rightarrow \mathbb{R}$ is positive definite (**PD**) if
* $V(z) > 0$ for all  $z$, $z \neq 0$ 
* $V(0)=0$ if and only if $z=0$
* all sublevel sets of $V$ are bounded. It is equivalent to $V(z) \rightarrow \infty$ as $z \rightarrow \infty$
#### Negative Definite Function
a function $V:\mathbb{R}^n \rightarrow \mathbb{R}$ is negative definite (**ND**) if
* $V(z) < 0$ for all  $z$, $z \neq 0$ 
* $V(0)=0$ if and only if $z=0$
#### Positive Semidefinite Function
a function $V:\mathbb{R}^n \rightarrow \mathbb{R}$ is positive semidefinite definite (**PSD**) if
* $V(z) \geq 0$ for all  $z$
* $V(0)=0$
#### Negative Semidefinite Function
a function $V:\mathbb{R}^n \rightarrow \mathbb{R}$ is negative semidefinite definite (NSD**) if
* $V(z) \leq 0$ for all  $z$
* $V(0)=0$