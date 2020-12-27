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


# References

* [Predictive Control - Borrelli, Bemporad, Marari](http://www.mpc.berkeley.edu/mpc-course-material)
