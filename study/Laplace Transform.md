---
date: 2024-09-06
tags:
  - theory
  - LaplaceTransform
title: "# Laplace transform"
source: "[[EE102. Introduction to Signals & Systems]]"
---
# Laplace transform
The Laplace transform converts **integral** and **differential** equations into **algebraic** equations.

This is like phasors, but
* applies to general signals, not just sinusoids
* handles non-steady-state conditions
## Definition
The Laplace transform of a signal (function) $f$ is the function $F = \mathcal{L}(f)$ defined by
$$
F(s) = \int_0^\infty f(t)e^{-st}dt
$$
for those $s \in C$ for which the integral makes sense

* $F$ is a complex-valued function of complex numbers,
* $s$ is called the (complex) frequency variable, with units sec$^{-1}$; $t$ is called the time variable (in sec); $st$ is unitless
* we assume $f$ contains no impulses at $t = 0$

**Common notation convention**: lower case letter denotes signal; capital letter denotes its Laplace transform, e.g., $U$ denotes $\mathcal{L}(u)$, $V_{in}$ denotes $\mathcal{L}(v_{in})$, etc.
## Examples
### Function $f(t) = e^t$
$$
F(s) = \int_0^\infty e^t e^{-st}dt = \int_0^\infty e^{(1-s)t}dt = \frac{1}{s-1}
$$
When
$$
\mathcal{L}(e^t) = \frac{1}{s-1}
$$
### Function $f(t) = 1$ (unit step)
$$
F(s) = \left.\int_0^\infty e^{-st}dt = -\frac{1}{s}e^{-st}\right\vert_0^\infty = \frac{1}{s}
$$

## Properties
### Linearity
if $f$ and $g$ are any signals, and $a$ is any scalar, we have
$$
\mathcal{L}(af) = aF, \mathcal{L}(f+g) = F + G
$$
### One-to-one property
the Laplace transform is one-to-one: if $\mathcal{L}(f) = \mathcal{L}(g)$ then $f = g$
* $F$ determines $f$
* inverse Laplace transform $\mathcal{L}^{−1}$ is well defined
## Derivative
if signal $f$ is continuous at $t = 0$, then
$$
L(f') = sF(s) - f(0)
$$
* time-domain differentiation becomes multiplication by frequency variable $s$ (as with phasors)
* plus a term that includes initial condition (i.e., $−f(0)$)

## Inverse Laplace transform
in principle we can recover $f$ from $F$ via
$$
f(t) = \frac{1}{2\pi j} \int_{\sigma-j\infty}^{\sigma+j\infty} F(s)e^{st}ds
$$
where $\sigma$ is large enough that $F(s)$ is defined for 

## Laplace Table

| Function $f(t)$        | $F(s) = \mathcal{L}[f(t)]$                               |
| ---------------------- | -------------------------------------------------------- |
| $f(t) = 1$             | $\displaystyle F(s)=\frac{1}{s}, s > 0$                  |
| $f(t) = e^{at}$        | $\displaystyle F(s) = \frac{1}{s-a}, s>a$                |
| $f(t)=t^n$             | $\displaystyle F(s) = \frac{n!}{s^{n+1}},s>0$            |
| $f(t)=\sin(at)$        | $\displaystyle F(s) = \frac{a}{s^2+a^2},s>0$             |
| $f(t)=\cos(at)$        | $\displaystyle F(s) = \frac{s}{s^2+a^2},s>0$             |
| $f(t)=\sinh(at)$       | $\displaystyle F(s) = \frac{a}{s^2-a^2},s>\|a\|$         |
| $f(t)=\cosh(at)$       | $\displaystyle F(s) = \frac{s}{s^2-a^2},s>\|a\|$         |
| $f(t)=e^{at}\sin(bt)$  | $\displaystyle F(s) = \frac{b}{(s-a)^2+b^2},s>\|a\|$     |
| $f(t)=e^{at}\cos(bt)$  | $\displaystyle F(s) = \frac{s-a}{(s-a)^2+b^2},s>\|a\|$   |
| $f(t)=e^{at}\sinh(bt)$ | $\displaystyle F(s) = \frac{b}{(s-a)^2-b^2},s-a>\|b\|$   |
| $f(t)=e^{at}\cosh(bt)$ | $\displaystyle F(s) = \frac{s-a}{(s-a)^2-b^2},s-a>\|b\|$ |
