---
title: "Model Predictive Control System Design and Implementation Using MATLAB by Liuping Wang"
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

# Discrete-Time MPC for Beginners
## Day-to-day Application Example of Predictive Control
The general design objective of model predictive control is to compute a trajectory of a future manipulated variable $u$ to optimize the future behavior of the plant output $y$. The optimization is done within a limited time window by givign plant information at the start time of the window. 

***Principle of MPC***

1. Moving horizon window
2. Prediction horizon
3. Receding horizon control
4. We require information at time $t_i$ (know the state $x(t_i)$) in order to predict the future.
5. A given model that describes the dynamics of the system
6. A criterion that reflects the current objective

## State Space Model with Embedded Integrator
### SISO System
Assume a single-input and single-output system of the form: 

$$
\begin{array}{c}
x_m(k+1) = A_m x_m(k) + B_m u(k) \\
y(k) = C_m x_m(k)
\end{array}
$$

By Taking the difference of $x_m (k) = A_m x_m (k-1) + B_m u(k-1)$ we get:

$$
\begin{array}{c}
\Delta x_m(k+1) = x_m(k+1) - x_m(k) \\
\implies 
\end{array}
$$


