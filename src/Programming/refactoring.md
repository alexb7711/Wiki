---
title: Refactoring: Improving the Design of Existing Code
header-includes:
	- \usepackage[a4paper, margin=0.5in]{geometry}
	- \fontfamily{qag} 
	- \renewcommand{\familydefault}{\sfdefault}
---

# Refactoring, A First Example
> When you find you have to add a feature to a program, and the program's code is not structured in a convenient way to add the feature, first refactor the program to make it easy to add the feature, then add the feature.

## The First Step in Refactoring
The first test is always to build a set of tests. The goal of having these tests upfront is so that if you make a mistake, you will hopefully catch it in one of the tests. Ideally these tests are self-checking.


