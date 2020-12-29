---
title: Predictive Control
header-includes:
    - \usepackage[a4paper, margin=0.5in]{geometry}
    - \usepackage{listings}
    - \lstset{breaklines=true}
    - \lstset{language=[Motorola68k]Assembler}
    - \lstset{basicstyle=\small\ttfamily}
    - \lstset{extendedchars=true}
    - \lstset{tabsize=2}
    - \lstset{columns=fixed}
    - \lstset{showstringspaces=false}
    - \lstset{frame=trbl}
    - \lstset{frameround=tttt}
    - \lstset{framesep=4pt}
    - \lstset{numbers=left}
    - \lstset{numberstyle=\tiny\ttfamily}
    - \lstset{postbreak=\raisebox{0ex}[0ex][0ex]{\ensuremath{\color{red}\hookrightarrow\space}}}
---
# Main Concepts
Model predictive control is the only advanced control technique that has see widespread impact on industrial process control. ***It's the only control technology that can deal with constraints***.

## Principles of Predictive Control
* Prediction
	* Why is prediction important: We care about the goal to be achieved more than what is currently happening within the system.

* Receding Horizon
	* What is receding horizon: Some fixed interval (period of time) over which we consider the future (Car headlight analogy).

## Optimization Problems
An optimization problem is generally formulated as

$$
inf_{z \in S \subseteq Z} f(z)
$$

Where $inf(\cdot)$ resembles finding the optimal value within the subset.

Solving this problem means to compute the least possible cost $f*$.

$$
f* = inf_{z \in S} f(z)
$$

The number $f*$ is the **optimal value** of $inf_{z \in S \subseteq Z} f(z)$, i.e.:

$$
f(z) \geq f(z*) = f* \forall z \in S, \; with \; z* \in S
$$

### Continuous Problems

***Nonlinear mathematical program***
$$
\begin{array}{lll}
inf_z                  & f(z)          & \\
subj. \; to            & g_i(z) \leq 0 & for \; i = 1,\cdots ,m \\
                       & h_j(z) = 0    & for \; j = 1,\cdots ,p \\
	               & z \in Z       & \\
\end{array}
$$

A point $\bar{z} \in \mathbb{R}^s$ is **feasible** for the continuous optimization problems if: 

1. it belongs to $Z$
2. It satisfies the inequality and equality constraints

### Integer and Mixed-Integer Problems
If the optimization problem 

$$
inf_{z \in S \subseteq Z} f(z)
$$

is finite, then the optimization problem is called *combinatorial* or *finite*. If $Z \subseteq {0,1}^s$, then the problem is said to be *integer*. If $Z$ is a subset of the Cartesian product of an integer set and real Euclidian space, then the problem is said to be *mixed-integer*. The standard form of a mixed-integer nonlinear program is: 

$$
\begin{array}{lll}
inf_{[z_c,z_b]}         & f(z_c,z_b)                                       & \\
subj. \; to             & g_i(z_c,z_b) \leq 0                              & for \; i = 1,\cdots ,m \\
                        & h_j(z_c,z_b) = 0                                 & for \; j = 1,\cdots ,p \\
	                & z_c \in \mathbb{R}^{s_c}, \; z_b \in {0,1}^{s_b} & \\
\end{array}
$$

## Convexity
***Theorem 1.1***

> Consider a convex optimization problem and let $\bar{z}$ be a local optimizer. Then $\bar{z}$ is a global optimizer. 

## Optimality Conditions
### Optimality Conditions For Unconstrained Problems

***Theorem 1.2*** (Necessary Condition):

> Suppose that $f:\mathbb{R}^s \rightarrow \mathbb{R}$ is differential at $\bar{z}$. If there exists a vector $d$ such that $\nabla f(\bar{z})'d < 0$, then there exists a $\delta > 0$ such that $f(\bar{z}+\lambda d) < f(\bar{z})$ for a $\lambda \in (0,\delta )$.

***Theorem 1.3*** (Sufficient Condition):

> Suppose that $f:\mathbb{R}^s \rightarrow \mathbb{R}$ is twice differentiable at $\bar{z}$. If $\nabla f(\bar{z}) = 0$ and the Hessian ($\nabla^2 f(\bar{z})$) of $f(z)$ at $\bar{z}$ is positive definite, then $\bar{z}$ is a local minimizer.

***Theorem 1.4***: (Necessary and Sufficient Condition):

> Supposed that $f:\mathbb{R}^s \rightarrow \mathbb{R}$ is differentiable at $\bar{z}$. If $f$ is convex, then $\bar{z}$ is a global minimizer iff $\nabla f(\bar{z}) = 0$

## Lagrange Duality Theory
Consider the optimality problem. Any feasible point $\bar{z}$ provides an upper bound to the optimal value $f(\bar{z}) \geq f*$ ($f*$ being the optimal value). The Lagrange Duality Theory generates a lower boundary for $f*$.

Starting from the same problem, we construct another problem with different variables and constrains. In other words, from the primal problem, we will develop the dual problem.

$$
L(z,u,v) = f(z) + u_1 g_1 (z) + \cdots + u_m g_m(z) + v_1 h_1(z) + \cdots + v_p h_p(z)
$$

# References

* [Predictive Control - Borrelli, Bemporad, Marari](http://www.mpc.berkeley.edu/mpc-course-material)
