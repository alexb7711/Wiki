---
title: Learn OpenGL - Graphics Programming
header-includes:
	- \usepackage[a4paper, margin=0.5in]{geometry}
	- \fontfamily{qag} 
	- \renewcommand{\familydefault}{\sfdefault}
---

# Creating A Window
Before we can start drawing graphics, we hvae to create a context for which OpenGL can start drawing. These operations are specific per operating system and OpenGL purposefully tried to abstract itself from these operations. This means that we have to create a window, define a context, and handle user input by ourselves.

Luckily there are plenty of libraries that provide the cross-platform functionality that we need. These libraries include GLUT, SDL, SFML, and GLFW. To create a window, look into the library specific instructions.

# Hello Triangle
In OpenGL everything is in 3D space. The process of transforming 3D coordinates to 2D pixels is managed by the graphics pipeline of OpenGL. The graphics pipeline can be divided into two large parts: the first transforms your 3D coordinates into 2D coordinates and the second part transforms the 2D coordinates into actual colored pixels.

