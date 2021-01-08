---
title: Model Predictive Control
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
1. Moving prediction horizon window
2. Receding horizon control that only executes the next step
3. Need for current-time information to make the next prediction
4. Model that describes the system dynamics used for prediction
5. Objective criterion based on measured difference between desired and actual response

# Model Choice for MPC
* Finite Impulse Response
* Step Response
* Transfer Function
* State-Space

## Finite Impulse Response
For single input single output (SISO) we write the convolution summation as:

$$
y_k = \sum_{i = 1}^N g_i u_{k-i}
$$

where $u_k$ and $y_k$ denote the input and output sequence elements respectively and $g_i$ compromise the first $N$ coefficients of an infinite Taylor Series. 

This model generalizes easily to the MIMO case by using matrices.

## Step Response
$$
h(z) = \sum_{i = 1}^{\infty} h_i z^{-1}
$$

where

$$
h(z) = \frac{g(z)}{\Delta (z)}
$$

and $\Delta (z)$ is the one-step difference operator $1-z^{-1}$.

## Transfer Function
Consider the SISO case:

$$
a(z) y_k = b(z) u_k
$$

where the form

$$
\frac{b(z)}{a(z)}
$$

gives a transfer function representation for the output-input ratio for the corresponding z-transforms.

## State Space
Assume a linearized, discrete-time, state-space model:

$$
\begin{array}{rl}
x(k+1) = & Ax(k) + Bu(k) \\
y(k)   = & C_y x(k)      \\
z(k)   = & C_z x(k)      \\
\end{array}
$$

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

### Constraint Categories
Constraints are three major types of constraints

1. Control variables Incremental Variation $u(k)$
	* Hard constraints on the size of the control signal movement (rate of change of the control variable $\Delta u(k)$)
$$
\Delta u^{min} \leq \Delta u(k) \leq \Delta u^{max}
$$
2. Control variables Amplitude $u(k)$
	* These are the most commonly encounters constraint. Similar to before:
$$
u^{min} \leq u(k) \leq u^{max}
$$

>> $u(k)$ is an incremental variable. For instance, if a value is allowed to open in the range between 15% and 80%, and the valve's normal operating value is at 30% then $u_{min} = 15% - 30% = -15%$ and $u_{max} = 80% - 30% = 50%$.

3. Output $y(k)$ or state variables $x(k)$.
	* We can specify the operating range for the plant output by stating: 
$$
y^{min} \leq y(k) \leq y^{max}
$$

>> Output constraints are often implemented as 'soft' constraints in the way that a slack variable $s_v > 0$ is added to the constraints: 

$$
y^{min} - s_v \leq y(k) \leq y^{max} + s_v
$$

>> Output constraints often cause a large change in both the control and incremental control variables when they are enforced (become active). When that happens, the control or incremental control can violate their own constraints. Implementing a slack variable 'relaxes' the constraint and helps in avoiding conflicts.

### MIMO Constraints
***Constraint for control movement***

$$
\begin{array}{l}
- (C_1 u(k_i - 1) + C_2 \Delta U) \leq -U^{min} \\
-(C_1 u(k_i - 1) + C_2 \Delta U) \leq U^{max}   \\
\end{array}
$$

Where $C_1$ is a column of identify matrices and $C_2$ is a square matrix of identity matrices that is incrementally added on each row.

***Constraint for increment control***

$$
\begin{array}{l}
- \Delta U \leq \Delta U^{min} \\
\Delta U \leq \Delta U^{max} \\
\end{array}
$$

***Output Constraint in terms of $\Delta U$***
$$
Y^{min} \leq Fx(k_i) + \Phi \Delta U \leq Y^{max}
$$

The model predictive control in the presence of hard constraints is proposed as finding the parameter vector $\Delta U$ that minimizes: 

$$
J = (R_s Fx(k_i))^T (R_s-Fx(k_i)) - 2 \Delta U^T \Phi^T (R_s Fx(k_i))+ \Delta U^T (\Phi^T \Phi + \bar{R}) \Delta U
$$

Subject to the inequality constraints (pg 52 Kiuping Wang):

$$
\begin{bmatrix}
M_1 \\
M_2 \\
M_3 \\
\end{bmatrix}
\Delta U \leq
\begin{bmatrix}
N_1 \\
N_2 \\
N_3 \\
\end{bmatrix}
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

## Lagrange Multipliers
To minimize the objective function subject to equality constraints, consider the Lagrange expression:

$$
J = 1/2 x^T Ex + x^T F + \lambda^T (Mx - \gamma)
$$

The process of minimizing is to take the partial derivative in terms of $x$ and $\lambda$, then equate these derivatives to zero.

$$
\begin{array}{l}
\lambda = -(ME^{-1}M^T)^{-1} (\gamma + ME^{-1}F) \\
x = -E^{-1} - E^{-1}M^T \gamma = x^{0} - E^{-1} M^T \gamma \\
\end{array}
$$

Where $x^{0} = -E^{-1} F$ is the global optimal solution that will give a minimum of the original cost function $J$ without constraints, and the second term is a correction term due to the equality constraints.

## Minimization with Inequality Constraints
The inequality constraint $Mx \leq \gamma$ may comprise of active ($M_i x = \gamma_i$) and inactive ($M_i x < \gamma_i$)where $M_i$ together with $\gamma_i$ form the $i^{th}$ inequality constraint and are the $i^{th}$ element of the $gamma$ vector.

### Kuhn-Tucker Conditions
$$
\begin{array}{l}
Ex + F + M^T \lambda = 0 \\
Mx - \gamma = 0 \\
\lambda^T (Mx - \gamma) = 0 \\
\lambda \geq 0 \\
\end{array}
$$

## Lagrange Duality Theory
The Lagrange multipliers are called dual variables in optimization literature. This method will lead to simple programming procedures for finding optimal solutions of constrained minimization problems. 

The primal problem is equivalent to $max_{\lambda \geq 0}min_{x}1/2 x^T Ex + x^T F + \lambda^T (Mx - \gamma)$. The minimization of $x$ is unconstrained and is attained by 

$$
x = -E^{-1}(F+M^T\lambda)
$$

Substituting x into the equation above we get the dual:

$$
\begin{array}{l}
max_{\lambda \geq 0} (-1/2 \lambda^T H \lambda - \lambda^T K - 1/2 F^TE^{-1}F)\\
H = ME^{-1}M^T \\
K = \gamma + ME^{-1}F \\
\end{array}
$$

Consider the optimality problem. Any feasible point $\bar{z}$ provides an upper bound to the optimal value $f(\bar{z}) \geq f*$ ($f*$ being the optimal value). The Lagrange Duality Theory generates a lower boundary for $f*$.

Starting from the same problem, we construct another problem with different variables and constrains. In other words, from the primal problem, we will develop the dual problem.

$$
L(z,u,v) = f(z) + u_1 g_1 (z) + \cdots + u_m g_m(z) + v_1 h_1(z) + \cdots + v_p h_p(z)
$$

## Strong Duality and Constrained Qualifications
If the cost of the dual problem is equal to the cost of the primary problem ($d* = f*$) then we have **strong duality**. In general, strong duality does not hold, even from convex primal problems (but can only hold if some suitable convexity conditions are satisfied). 

***Slater's Condition***:

> Consider the optimality problem stated above. There exists a $\hat{z} \in \mathbb{R}^s$ which belongs to the relative interior of the problem domain $Z$, which is feasible ($g(\hat{z}) \leq 0, h(\hat{z}) = 0$) and for which $g_j (\hat{z}) < 0$ for all $j$ for which $g_j$ is not an affine function.


***Theorem 1.5*** (Slater's Theorem):

> Consider the primal and its dual problem. If the primal problem is convex, Slater's condition holds and $f*$ is bounded then $d* = f*$.

Recall that this is for the unconstrained problem.

### Karush-Kuhn-Tucker Conditions
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

# Linear and Quadratic Optimization
## Linear Programming
When the cost and constraints of the continuous optimization problem are affine, the problem is called a linear program. The most general form is:

$$
\begin{array}{lll}
inf_z                  & c'z       \\
subj. \; to            & Gz \leq w \\
\end{array}
$$

Where $G \in \mathbb{R}^{m\times s},\; w \in \mathbb{R}^m$.

### Geometric Interpretation and Solution Properties
Consider the Linear Program above and suppose:

$$
Z* = argmin_{z \in P} c'z
$$

where $Z*$ is set of optimizer and $f*$ is the optimal value. There are three cases that can occur:

1. The LP is unbounded ($f* = - \infty$)
2. The LP solution is bounded ($f* > - \infty$ and the optimizer is unique. $z* = Z*$ is a singleton.
3. The LP solution is bounded and there are multiple optima. $Z*$ is an subset of $\mathbb{R}^s$ which can be bounded or unbounded.

### Dual of LP
Consider the primary LP given above. The dual is written as; 

$$
\begin{array}{lll}
inf_z                   & -u'w      \\
subj. \; to             & -G'u = -c \\
                        & u \geq 0  \\
\end{array}
$$

**Note that LP's feasibility implies strong duality**.

### KKT Conditions for LP
$$
\begin{array}{rll}
G'u+c = 0             &                  \\
u_i (G_i z - w_i) = 0 & i = 1, \cdots, m \\
u \geq 0              &                  \\
Gz-w = 0              &                  \\
\end{array}
$$

### Active Constraints and Degeneracies
***Definition***

> We say that Linear Independence Constraint Qualification (LICQ) holds at $z*$ if the matrix $G_{A(z*)}$ has full row rank.

Where 

$$
\begin{array}{rcl}
A(z)                     & = & \{i \in I: G_i z = w_i\} \\
NA(z)                    & = & \{i \in I: G_z < w_i\}   \\
\end{array}
$$

$NA$ standing for Not Active constraint and $A$ standing for active constraint.

$$
\begin{array}{rcl}
G_{A(z*)}z*              & = & w_{A(z*)}  \\
G_{NA(z*)}z* 		 & < & w_{NA(z*)} \\
\end{array}
$$

**A violation of LICQ is equivalent to having more than $s$ constraints active at an optimal vertex.**

***Definition 2.2***

> The LP is said to be a primal degenerate if there exists a $z* \in Z*$ such that the LICQ does not hold at $z*$.

***Definition 2.3***

> The LP is said to be dual degenerate if its dual problem is primal degenerate.

***Lemma 2.2***

> If the primal problem is not degenerate then the dual problem has a unique optimizer. If the dual problem is not degenerate, then the primal problem has a unique optimizer. Multiple dual optimizers imply primal degeneracy and multiple primal optimizers imply dual degeneracy. The reverse is not true. 

Generally, the statement "if the dual problem is primal degenerate then the primal problem as multiple optima" is not true.

## Quadratic Programming
### Continuous Case (Borrelli, Bemporad, Marari)
The continuous problem is called a quadratic problem if the constraint functions are affine and the cost function is a convex quadratic function.

It generally takes the form of 

$$
\begin{array}{cl}
min_z         & 1/2 z' Hz + q'z + r \\
subject \; to & Gz \leq w \\
              & Az = 0
\end{array}
$$

Where $H = H^T \succ 0 \in \mathbb{R}^{s\times s}$. The level curves, created by the cost function above, draw ellipsoids. The smaller the ellipsoid, the smaller the cost $k_i$. Since $H$ is strictly positive definite, the quadratic program cannot have multiple optima or unbounded solutions. If $P$ is not empty ($P$ being the feasible set), then the solution is unique.

1. The optimizer lies strictly inside the feasible polyhedron
2. The optimizer lies on the boundary of the feasible polyhedron

The objective function $J$ and the constraints are expressed as:

$$
\begin{array}{l}
J = 1/2 x^T Ex + x^T F \\
Mx \leq \gamma \\
\end{array}
$$

Without loss of generality $E$ can be assumed to be symmetric and positive definite.

# Individual Notes
[Model Predictive Control System Design and Implementation Using MATLAB® by Liuping Wang](mpcsysdesignusingmatlab)
[Predictive Control by Borelli, Bemporad, and Morari](predictivecontrolforlinearandhybridsys)

# References

* [Predictive Control - Borrelli, Bemporad, Marari](http://www.mpc.berkeley.edu/mpc-course-material)
* [Model Predictive Control System Design and Implementation Using MATLAB - Jiuping Wang]()
