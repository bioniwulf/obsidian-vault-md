# Lyapunov Theorems
Lyapunov theory is used to make conclusions about trajectories of a system $\dot{x}=f(x)$ (e.g., G.A.S.) without finding the trajectories (i.e., solving the differential equation).
a typical Lyapunov theorem has the form:
* **IF** there exists a function $\dot{V}:\mathbb{R}^n \rightarrow \mathbb{R}$ that satisfies some conditions on $V$ and $\dot{V}$
* **THEN**, trajectories of system satisfy some property
if such a function $V$ exists we call it a **Lyapunov function** (that proves the property holds for the trajectories).
Lyapunov function $V$ can be thought of as generalized energy function for system.
## A Lyapunov Boundedness Theorem
**IF** there is a function $V$ that satisfies
* all sublevel sets of $V$ are bounded
* $\dot{V}(z) \leq 0$ for all $z$
**THEN** all trajectories are bounded, i.e., for each trajectory $x$ there is an $R$ such that  $||x(t)|| \leq R$ for all $t \geq 0$.
In this case, $V$ is called a **Lyapunov function** (for the system) that proves the trajectories are bounded.
## A Lyapunov G.A.S. Theorem
**IF** there is a function $V$ that satisfies
* $V$ is positive definite
* $\dot{V}(z)<0$ for all $z\neq0$, $\dot{V}(0)=0$
**THEN**, every trajectory of $\dot{x}=f(x)$ converges to zero as $t \rightarrow \infty$

Interpretation:
* V is positive definite generalized energy function
* energy is always dissipated, except at 0
## A Lyapunov Exponential Stability Theorem
**IF** there is a function $V$ and constant $\alpha>0$ that satisfies
* $V$ is positive definite
* $\dot{V}(z)<-\alpha V(z)$ for all $z$
**THEN**, there is an $M$ such that every trajectory of $\dot{x}=f(x)$ satisfies
$$
||x(t)|| \leq Me^{-\alpha t/2}||x(0)||
$$
This called global exponential stability (G.E.S.)