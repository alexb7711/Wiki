---
title: "Predictive Control for Linear and Hybrid Systems"
author: 
    - Borrelli
    - Bemporad
    - Morari
    - Alexander Brown
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

$\bar{z}$ is also a *local optimizer* or *local minimizer* if it satisfies the constraints above as well as $||z - \bar{z}|| \leq R$ where $R$ defines a region (think of stability definitions Linear Multi-Variable Control).

***Active, Inactive, and Redundant Cases***: 
Consider a feasible point. $g_i(\bar{z}) = 0$ is active,$ g_i(\bar{z}) < 0$ is inactive, and a constraint is redundant if removing the constraint does not change the feasible set $S$.

***Eliminating Equality Constraints***:
The simplest way to remove equality constraints is to replace them with two inequalities:

$$
\begin{array}{l}
h_i(z) = 0 \\
\therefore is\;replaced\;by \\
h_i (z) \leq 0 \\
-h_i (z) \leq 0 \\
\end{array}
$$

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
The standard optimization problem is said to be convex if the cost function $f$ is convex on $Z$ *and* $S$ is a convex set. A fundamental property of convex optimization problems is that local optimizers are also global optimizers (think calculus optimization: min/max of parabola is global).

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

The primal problem is written as the problem:

$$
\mathop{sup}_{(u,v), u \geq 0} \mathop{inf}_{z\inZ}L(z,u,v) \leq \mathop{inf}_{s\in Z,g(z) \leq0, h(z) = 0} f(z)
$$

Suppose we define $d(u,v) = \mathop{inf}_{z\inZ}L(z,u,v)$, then we can restate the previous problem as:

$$
\mathop{sup}_{(u,v), u \geq 0} d(u,v)
$$

where its optimal solution, assuming it exists, is denoted by $(u*,v*)$. The dual cost $d(u,v)$ is the optimal solution of the *unconstrained optimization problem*. A point $(u,v)$ is dual feasible if $u \geq 0$ and $d(u,v) \geq 0$. $d(u,v)$ is *always a concave function* since it is the pointwise infimum of a family of affine functions of $(u,v)$. This implies that the *dual problem is a convex optimization problem even if the original problem is not convex*. In general, however, the solution to the dual problem is only a lower bound of the primal problem (known as *weak duality*). In other words there is a gap between the primal and dual solutions.

![Weak and Strong Duality](https://external-content.duckduckgo.com/iu/?u=https%3A%2F%2Foptimization.mccormick.northwestern.edu%2Fimages%2F0%2F01%2FDualityOptimalityGap.JPG&f=1&nofb=1)
The difference $f* - d*$ is the duality gap, where $f*$ and $d*$ are the optimal solutions of both the primal and dual problem respectively.

## Strong Duality and Constraint Qualifications
If the cost of the dual problem is equal to the cost of the primary problem ($d* = f*$) then we have **strong duality**. In general, strong duality does not hold, even from convex primal problems (but can only hold if some suitable convexity conditions are satisfied). *Constraint Qualifications are conditions on the constraint functions which imply strong duality for convex problem*.

***Slater's Condition***:

> Consider the optimality problem stated above. There exists a $\hat{z} \in \mathbb{R}^s$ which belongs to the relative interior of the problem domain $Z$, which is feasible ($g(\hat{z}) \leq 0, h(\hat{z}) = 0$) and for which $g_j (\hat{z}) < 0$ for all $j$ for which $g_j$ is not an affine function.

***Theorem 1.5*** (Slater's Theorem):

> Consider the primal and its dual problem. If the primal problem is convex, Slater's condition holds and $f*$ is bounded then $d* = f*$.

Recall that this is for the unconstrained problem.

### Certificate of Optimality
Without knowing the exact value of $f*$ we can give a bound on how suboptimal a given feasible point is. In fact, if $z$ is primal feasible and $(u,v)$ is dual feasible then $d(u,v) \leq f* \leq f(z)$. Therefore $z$ is $\epsilon$-suboptimal, with $\epsilon = f(z) - d(u,v)$ (primal-dual gap). Therefore many algorithms utilize

$$
f(z_k) - d(u_k, v_k) < \epsilon_k
$$

for the termination condition. This condition at the worst supplies $\epsilon$-suboptimal. If strong duality holds, the condition can be met for arbitrarily small tolerances (will converge to the exact solution).

## Complimentary Slackness
The complimentary slackness is represented as:

$$
u_i * g_i(z*) = 0, \; i = 1, \cdots, m
$$

and it can be interpreted as follows. If the $i$-th inequality constraint of the primal problem is inactive at the optimum ($g_i (z*) < 0$), then the $i$-th dual optimizer has to be zero ($u* = 0$). Vice versa, if the $i$-th dual optimizer is different from zero ($u* > 0$), then the $i$-th constraint is active at the optimum ($g_i (z*) = 0).

## Karush-Kuhn-Tucker Conditions
The Primal and dual optimal pair $z*,\;(u*,v*)$ of an optimization problem with differentiable cost and constraints and zero duality gap, have to satisfy the following conditions:

$$
\begin{array}{rll}
\nabla f(z*) + \sum_{i} u_i * \nabla g_i (z*) + \sum_j v_j * \nabla h_j (z*) = 0 &                   \\
u_i * g_i (z*) = 0                                                               & i = 1, \cdots , m \\
u_i * \geq 0                                                                     & i = 1, \cdots , m \\
g_i (z*) \leq 0                                                                  & i = 1, \cdots , m \\
h_j (z*) = 0                                                                     & j = 1, \cdots , p \\
\end{array}
$$

Where: 

* $g_i (z*) \leq 0$ and $h_j (z*) = 0$ are the primal feasibility conditions
* $u_i * \geq 0$ is the dual feasibility condition
* $u_i * g_i (z*) = 0$ is the complimentary slack condition

***Theorem 1.6***

> Consider the primal optimization problem. Also suppose the problem is convex and that cost and constraints $f$, $g_i$, and $h_i$ are differentiable and feasible $z*$. If the problem satisfies Slater's condition then $z*$ is optimal iff there are $(u*, v*)$ that, together with $z*$, satisfy the KKt conditions.

**If a convex optimization problem with differentiable objective and constraint functions has linearly independent set of active constraint gradients, then the KKT conditions provide necessary and sufficient conditions for optimality.**

***Theorem 1.7***

> Consider the primal problem and let $Z$ be a nonempty open set of $\mathbb{R}^s$. Let $z*$ be a feasible solution and $A = {i: g_i (z*) = 0}$ be the set of active constraints at $z*$. Suppose cost and constraints $f$ and $g_i$ are differentiable at $z*$ for all $i$ and that $h_j$ are continuously differentiable at $z*$ for all $j$. Further, suppose that $\nabla g_i (z*)$ for $i \in A$ and $\nabla h_j (z*)$ for $j = 1, \cdots, p$, are linearly independent. If $z*$, $(u*,v*)$ are primal and dual optimal points, then they satisfy the KKT conditions. In addition, if the primal problem is convex, the $z*$ is optimal iff there are $(u*,v*)$ that, together with $z*$, satisfy the KKT conditions.

# Linear and Quadratic Optimization
## Linear Programming
When the cost and the constraints of the continuous optimization problem are affine, then the problem is called a *linear program*. The most general form of a LP is:

$$
\begin{array}{l}
inf_z            & c'z \\
subject\;to      & Gz \leq w \\
$$

Two other common forms are:

$$
\begin{array}{l}
inf_z            & c'z \\
subject\;to      & Gz \leq w \\
                 & Az = b \\
$$

and 

$$
\begin{array}{l}
inf_z            & c'z \\
subject\;to      & Gz \leq w \\
                 & z \geq 0 \\
$$

By standard manipulations, it always possible to convert one of the three forms into the other.

## Geometric Interpretation and Solutions Properties
Three cases can occur when solving an LP

1. The solution is unbounded $f* = - \infty$
2. The solution is bounded $f* > - infty$ and the optimizer is unique ($z* = Z*$ is a singleton)
3. The solution is bounded and there are multiple optima $Z*$ is a subset of $\mathbb{R}^s$ which can be either bounded or unbounded.

## Dual of LP
Consider the LP

$$
\begin{array}{l}
inf_z & c'z \\
subject\;to & Gz \leq w \\
\end{array}
$$

The dual problem is written as:

$$
\begin{array}{l}
sup_u            & -u' w \\
subject\;to      & -G' u = c \\
                 & u \geq 0 \\
\end{array}
$$

## KKT condition for LP
$$
\begin{array}{rll}
G'u + c = 0           & \\
u_i (G_i z - w_i) = 0 & i = 1, \cdots, m\\
u \geq 0              & \\
Gz - w \leq 0         & \\
\end{array}
$$

## Active Constraints and Degeneracies
Suppose we have a matrix of constraints $G$, we can decompose that matrix into active and inactive sections (think observable decomposition from Multi-Variable Control):

$$
\begin{array}{l}
A(z) = {i \in I : G_i z = w_i } \\
NA(z) = {i \in I : G_i z < w_i } \\
\end{array}
$$

***Definition 2.1***: (Linear Independence Constraint Qualification (LICQ)

> We say the LICQ holds at $z*$ if the matrix $G_{A(z*)}$ has full row rank.

***Lemma 2.1***

> Assume that the feasible set $P$ of a primal LP is bounded. If the LICQ is violated at $z_1 * \in Z*$ then there exists a $z_2 * \in Z*$ such that $|A(z_2 *)| > s$.

Therefore, violation of LICQ is equivalent to having more than $s$ constraints active at an optimal vertex.

***Definition 2.2***

> The primal LP is said to be primal degenerate if there exists a $z* \in Z*$ such that LICQ does not hold at $z*$

***Definition 2.3***

> The primal LP is said to be dual degenerate if the dual problem is primal degenerate

***Lemma 2.2***

> If the primal problem is not degenerate then the dual problem has a unique optimizer. If the dual problem is not degenerate, then the primal problem has a unique optimizer.

## Quadratic Programming
The continuous optimization problem is called a quadratic program (QP) if the constraint functions are affine and the cost function is a convex quadratic function. QPs can be represented in the general form:

$$
\begin{array}{l}
min_z       & 1/2 z' H z + q'z + r \\
subject\;to & Gz \leq w \\
\end{array}
$$

or 

$$
\begin{array}{l}
min_z       & 1/2 z' H z + q'z + r \\
subject\;to & Gz \leq w \\
            & Az = b
\end{array}
$$

### Geometric Interpretation and Solution Properties
The two dimensional geometric interpretation is depicted as ellipsoid level curves (calculus 3: partial derivatives being visualized). All the points $z$ belonging to both the ellipsoid (cost function) and the polyhedron (feasible set) are feasible points with an associated cost $k$. The smaller the ellipsoid, the smaller is its cost $k_i$. This amounts to finding a feasible $z$ which belongs to the level curve with the smallest $k_i$. Since $H$ is strictly positive definite, the QP cannot have multiple optima nor unbounded solutions. If $P$ (the feasible set) is not empty, the optimizer $z$ is unique. This results in two cases:

1. The optimizer lies strictly inside the feasible polyhedron
2. The atomizer lies on the boundary of the feasible polyhedron


