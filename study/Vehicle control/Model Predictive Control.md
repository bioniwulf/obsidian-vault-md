# Model Predictive Control

## Overview
Classical controllers, such as PID controllers, bang-bang controllers, or state controllers, only consider past and current system behavior (i.e. they are “reactive” to a deviation). Predictive controllers use a system model to **predict the future behavior** anticipating deviations from the reference.

MPC is based on a repeated real-time optimization of a mathematical system model. Based on this system model, the MPC predicts the future system behavior considering it in the optimization that determines the optimal trajectory of the manipulated variable $u$ (the system input).

![[MPC Simplified Scheme.png]]
**Simplified block diagram of a MPC-based control loop**

MPC is a set of advanced control methods, which explicitly use a model to predict the future behavior of the system. Taking this prediction into account, the MPC determines an optimal output u by solving a constrained optimization problem. It is one of the few control methods that directly considers constraints. Often, the cost function is formulated in such a way that the system output $\boldsymbol{y}$ tracks a given reference $\boldsymbol{r}$ for a horizon $N_2$. **Only the first value of the optimized output trajectory is applied to the system**. This prediction and optimization is repeated in each time instance. This is why MPC is also referred to as **“receding horizon”** control. **In essence**, the idea is that a short-term (predictive)
optimization achieves optimality over a long time.

![[MPC Time Diagram.png]]

The prediction horizon $N_2$ must be long enough to represent the effect of a change in the manipulated variable $u$ on the control variable $y$. Delays can be considered by the lower prediction horizon $N_1$ or by incorporating them into the system model.

**Assuming an arbitrary system**:
$$
\begin{matrix*}[l]
\boldsymbol{x}(\boldsymbol{k}+1) = \boldsymbol{f}(\boldsymbol{x}(\boldsymbol{k}),\boldsymbol{u}(\boldsymbol{k})) \\
\boldsymbol{y}(\boldsymbol{k}) = \boldsymbol{g}(\boldsymbol{x}(\boldsymbol{k}))
\end{matrix*}

$$

MPC minimizes a user-defined cost function $J$ , e.g. the tracking error between the reference vector $\boldsymbol{r}$ and the model output $\boldsymbol{y}$:
$$
\begin{matrix}
\displaystyle
\min_u J(\boldsymbol{x}(\boldsymbol{k}),\boldsymbol{u}(\boldsymbol{k})) =
\min_u \sum_{i=N_1}^{N_2}\| \boldsymbol{r}(\boldsymbol{k}+1|\boldsymbol{k}) -
\boldsymbol{y}(\boldsymbol{k}+1|\boldsymbol{k}) \|, \\
s.t. \\
\boldsymbol{u}_{lb} \leq \boldsymbol{u}(\boldsymbol{k}+j|\boldsymbol{k}) \leq  \boldsymbol{u}_{ub} \\
\boldsymbol{y}_{lb} \leq \boldsymbol{y}(\boldsymbol{k}+i|\boldsymbol{k}) \leq  \boldsymbol{y}_{ub} \\
\forall i \in \{N_1,\ldots,N_2\} \text{ and } j \in \{0, \ldots, N_u\}

\end{matrix}
$$
This formulation uses an arbitrary norm $\|\cdot\|$ (it could be $L_2$ and $L_\infty$ as well).
The $\boldsymbol{x}(\boldsymbol{k}+1|\boldsymbol{k})$ is the predicted state $\boldsymbol{k}+1$ at the time point $\boldsymbol{k}$.

One has to distinguish several aspects of MPC:
* feasibility of the open-loop optimization problem,
* stability of the closed-loop controller, and
* robustness regarding uncertainties.
The **first** concerns the formulation of the optimization problem, the **second** the controller as a whole with regard to disturbances, and the **last** mainly the accuracy of the process model.
### MPC Feasibility
Hard input constraints (on $\boldsymbol{u}$) represent physical limitations of, e.g. actuators, which in fact must not be violated. In contrast, hard output constraints (on $\boldsymbol{y}$) are often rather desired than required. They may render the optimization problem infeasible. Relaxing these output constraints by introducing slack variables $\boldsymbol{\xi}$ to the optimization problem creates an extra degree of freedom. 
$$
\begin{matrix}
\displaystyle
\| \boldsymbol{r}(\boldsymbol{k}+1|\boldsymbol{k}) -
\boldsymbol{y}(\boldsymbol{k}+1|\boldsymbol{k}) \|_{W_w} + \| \boldsymbol{\xi}(\boldsymbol{k}+1|\boldsymbol{k})_{W_\xi} \|, \\
s.t. \\
\boldsymbol{u}_{lb} \leq \boldsymbol{u}(\boldsymbol{k}+j|\boldsymbol{k}) \leq  \boldsymbol{u}_{ub} \\
\boldsymbol{y}_{lb} - \boldsymbol{\xi}(\boldsymbol{k}+1|\boldsymbol{k}) \leq \boldsymbol{y}(\boldsymbol{k}+i|\boldsymbol{k}) \leq  \boldsymbol{y}_{ub}-\boldsymbol{\xi}(\boldsymbol{k}+1|\boldsymbol{k}) \\
\forall i \in \{N_1,\ldots,N_2\} \text{ and } j \in \{0, \ldots, N_u\}

\end{matrix}
$$
Nevertheless, the input constraints are still hard and turn the optimization problem to be non-linear A nonfeasible desired trajectory $w$ provokes instabilities. To tackle the problem of unfeasible desired trajectories, it's suggested to filter the trajectory $w$ generating a feasible reference trajectory $r$. This approach was called “reference governor”. It avoided constraint violations on the input by adjusting the desired trajectory beforehand with regard to the response behavior of the plant.
### MPC Stability
In its most basic formulation, stability is the property of a system that a bounded input results in a bounded output: **the BIBO stability**. In case that the transient behavior converges against an equilibrium, the closed-loop system is called to be asymptotically stable.

However, finite prediction horizon obviously is an extreme restriction. Computational restrictions limit the MPC in general to a finite horizon. To still guarantee asymptotic stability, the optimal cost function of the MPC must be monotonically decreasing over time.

The cost J is not explicitly a function of time, so the desired monotonically decreasing behavior over time needs to be artificially imposed on it. One way to do this is to formulate an optimization problem that the control function is bounded by a [[Lyapunov Function]].
A [[Lyapunov Function]] function is a continuously differentiable scalar function $V(\boldsymbol{x}): \mathbb{R}^n \rightarrow \mathbb{R}$  with $V(0)=0$. It is always positive and does not increase over time:
* $V(\boldsymbol{x}) = 0, \forall \boldsymbol{x} \neq 0$
* $\dot{V}(\boldsymbol{x}) \leq 0, \forall \boldsymbol{x} \neq 0$
The [[Lyapunov Theorem]] essentially defines a prototypical function resulting in a bounded system state over time. Thus, the state of the art for stability schemes for (non-linear) MPC is to define the cost function in such a way that the optimal cost behaves as a [[Lyapunov Function]] - or to prove this to be the case respectively. For this purpose, the optimization problem is extended by additional cost terms or constraints.
**One approach** to make the optimal cost $J^0$ behave like a [[Lyapunov Function]] is to introduce a terminal cost $J(\boldsymbol{k} + N_2)$. This nullifies the advantage of an infinite horizon, since the cost stays the same until infinity $J(\boldsymbol{k} + N_2) \approx J(\infty)$. **Whereby**, more constraints to guarantee stability of the controller may again cause feasibility problems of the optimization—especially for short prediction horizons. **Therefore**, it is common practice to constraint a terminal region instead of, e.g. a zero terminal constraint $\| \boldsymbol{x}(\boldsymbol{k} + N_2) \| = 0$.

**The most common stability approach**, which avoids a [[Lyapunov Function]], is to introduce so-called “**contraction constraints**” ensuring that (usually the euclidean norm of) the state vector is decreasing over time:
$$
\| \boldsymbol{x}(\boldsymbol{k} + 1|\boldsymbol{k}) \| \leq \| \boldsymbol{x}(\boldsymbol{k}) \|
$$
## Main advantages
* The method can explicitly consider control and controllable system constraints. It is one of the few control methods that directly considers constraints.
* The MPC controller achieves optimal control.

## Main Disadvantages
* Necessary to build controllable object model (linear or nonlinear).
* Calculation complexity (in 20-50 times slower in comparison with PID and others).
* Software Requirement complexity. Mostly it's necessary to add 3rd-party libraries for solving optimization problem.

## Study Materials
* [Youtube. Understanding Model Predictive Control](https://www.youtube.com/playlist?list=PLn8PRpmsu08ozoeoXgxPSBKLyd4YEHww8)
* [Youtube. Model Predictive Control - Part 1: Introduction to MPC (Lasse Peters)](https://www.youtube.com/watch?v=XaD8Lngfkzk)
* [Youtube. Model Predictive Control - Part 2: Numerical Methods for MPC (Lasse Peters)](https://www.youtube.com/watch?v=TtGCEzYxM_A)
## Software
* [Model predictive control python toolbox](https://www.do-mpc.com/en/latest/index.html)
## Books Revolved around
* [[Model Predictive Control. Theory, Computation, and Design]]
## Article Review
* [[Review on model predictive control. An engineering perspective]]
* [[Model predictive control. Past, present and future]]
* [[Model predictive control. Theory and practice]]
* [[Tutorial overview of model predictive control]]
## Case Study for Underwater Vehicle
* [[Experimental Evaluation on Depth Control Using Improved Model Predictive Control for AutonomouscUnderwater Vehicle (AUVs)]]
* [[Model predictive control for an AUV with dynamic path planning]]
* [[Path Following Control for Autonomous Ship using Model Predictive Control]]
* [[Trajectory Tracking Control of an Autonomous Underwater Vehicle Using Lyapunov-Based Model Predictive Control]]