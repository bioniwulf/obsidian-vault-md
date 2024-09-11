# Lyapunov Theorems
Lyapunov theory is used to make conclusions about trajectories of a system $\dot{x}=f(x)$ (e.g., G.A.S.) without finding the trajectories (i.e., solving the differential equation).
a typical Lyapunov theorem has the form:
* **IF** there exists a function $\dot{V}:\mathbb{R}^n \rightarrow \mathbb{R}$ that satisfies some conditions on $V$ and $\dot{V}$
* **THEN**, trajectories of system satisfy some property
if such a function $V$ exists we call it a **Lyapunov function** (that proves the property holds for the trajectories).
Lyapunov function $V$ can be thought of as generalized energy function for system.

**Basically** Liapunov’s second method is a generalization of the physical principles that for a conservative system: (1) a rest position is stable if the potential energy is local minimum, otherwise it is unstable, and (2) the total energy is a constant during any motion.

Without loosing generality we will consider that equilibrium point of the function located in the center ($x=0$), if not we can change $x \rightarrow x'$ that satisfies this assumption. q
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
## Finding Lyapunov functions
* there are many different types of Lyapunov theorems
* the key in all cases is to find a Lyapunov function and verify that it has the required properties
* there are several approaches to finding Lyapunov functions and verifying the properties

One common approach:
* decide form of Lyapunov function (e.g., quadratic), parametrized by some parameters (called a Lyapunov function candidate)
* try to find values of parameters so that the required hypotheses hold

Other sources of Lyapunov functions:
 * value function of a related optimal control problem
 * linear-quadratic Lyapunov theory
 * computational methods
 * converse Lyapunov theorems
 * graphical methods