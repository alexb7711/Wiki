---
title: Linear Multi-Variable Control
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
# An Introduction Into Optimal Control Theory
## Statement of the Optimal Control Problem
A mathematical statement of the optimal control problem consists of:

1. A description of the system to be controlled
2. A description of the system constraints and possible alternatives
3. A description of the task to be accomplished
4. A statement of the criterion of optimal performance

The most general continuous performance criteria to be considered is: 

$$
J = S(x(t_f), t_f) + \int_{t_0}^{t_f} L(x(t), u(t), t) \; dt
$$

* $S$ is the cost or penalty associated with the error in stopping or terminal state at time $t_f$.
* $L$ is the cost or loss function associated with the transient state errors and control effort.

### Examples

* $S = 0$ and $L = u^T u$

$$
J = \int_{t_0}^{t_f} u^T u \; dt
$$

> is a measure of the control effort expended. In many cases this term can be interpreted as control energy. This called the least-effort problem.

* $S = [x(t_f) - x_d]^T [x(t_f) - x_d]$ and $L = 0$, minimizing $J$ is equivalent to minimizing the square of the norm of the error between the final state $x(t_f)$ and the desired final state $x_d$. This is the minimum terminal error problem.

* $S = 0$ and $L = [x(t) - \eta (t)]^T [x(t) - \eta (t)]$. Then minimizing $J$is equivalent to minimizing the integral norm squared of the transient error between the actual state trajectory $x(t)$ and desired trajectory $\eta (t)$.

* A general quadratic criterion which gives a weighted trade-off between the previous three criteria uses $S = [x(t_f) - x_d]^T M[x(t_f) - x_d]$ and $L = [x(t) - \eta (t)]^T Q[x(t) - \eta (t)]$. The $n \times n$ weighting matrices $M$ and $Q$ are assumed to be positive semidefinite to ensure a well-defined for finite minimum $J$. The $r \times r$ matrix $R$ is assumed to be positive definite because $R^{-1}$ will be required in future manipulations. Values for $M$, $Q$, and $R$ should be selected to give the desired trade-offs among terminal error, transient error, and control effort.

If the system is completely controllable, there is at least one control which will transfer any initial state to any desired final state. If the system is not controllable, it it not meaningful to search for the optimal control. However, controllability does not guarantee that a solutions exists for every optimal control problem. Whenever the admissible controls are restricted to the set $U$, certain final state may not be attainable. Even though the system is completely controllable, the required control may not belong to $U$.

# Resources
* [Modern Control Theory - Brogan]()
* [Linear Systems Theory - Hespanha]()
