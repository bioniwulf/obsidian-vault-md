---
date: 2024-09-09
title: "# Lyapunov Stability Theorem"
tags:
  - theory
  - Lyapunov
  - Stability
source: https://www.youtube.com/watch?v=Fb6XY-cTivo&feature=youtu.be
notation: "[[Stability Definitions]]"
---
# Lyapunov Stability Theorem
The origin is the stable equilibrium point of $\dot{\boldsymbol{x}} = f(\boldsymbol{x})$ if there there exists $r>0$ and **PD** function $V(\boldsymbol{x})$ on $B_r(\boldsymbol{0})$ such that $\dot{V}(x)$ is **NSD** on $B_r(\boldsymbol{0})$.
Moreover, if $\dot{V}$ is **ND** on $B_r(\boldsymbol{0})$, then the origin is asymptotically stable.

$\dot{V}(x)$ can be calculated using the chain rule as
$$
\dot{V}(x) = \frac{dV}{dt}=\nabla V f(x)
$$

This theorem only provides a **sufficient** stability conditions. If $V$ can not be found, **it doesn't** mean that there is no stable equilibrium point. 
