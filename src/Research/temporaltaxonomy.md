---
title: "A taxonomy for task allocation problems with temporal and ordering"
header-includes:
    - \usepackage[a4paper, margin=0.5in]{geometry}
    - \fontfamily{qag} 
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

# Taxonomy
## ST-SR-TA-TW
### Hard Constraints
* Typically assume there are more tasks than robots and the tasks are known in advance
* Require time extended assignments and have time window constraints on task
* Composed of two sub-problems
	* Assignment problem to find the assignment that optimizing the objective function
	* Task sequencing problem to find feasible orderings of tasks that result in optimal assignment
	* Scheduling problem to assign times to tasks in a way the optimize the objective function
