---
title: Game Architecture
header-includes:
	- \usepackage[a4paper, margin=0.5in]{geometry}
---

# Engine Support Systems
Every game engine requires some low-level support systems that manage mundane tasks, such as starting up and shutting down the game, configure game features, managing memory usage, access to the file system, providing access to the different types of assets the game may use.

## Subsystem Startup and Shutdown
In C++, global and static objects are constructed before the program's entry point (`main()`). However, these constructors are called in a totally unpredictable order. The destructors of global and static class instances are called after `main()` returns, and once again they are called in an unpredictable order. This method is not desireable for initializing and shutting down the subsystems of a game engine.

This is unfortunate because a common pattern for implementing major subsystems, such as the ones that make up the game engine, are defined as singleton classes (often called a manager). 

### Construction on Demand
There is a little trick that can be employed to time the creation of static variables. A static variable that is declared within a function will not be constructed before `main()`, but rather on the first invocation of that function. So if our global singleton is function-static, we can control the order of construction of our global singletons as seen in Figure \ref{fig:controlledSingleton}.

![Controlled singleton creation in C++ \label{fig:controlledSingleton}](https://learning.oreilly.com/library/view/game-engine-architecture/9781466560017/images/ilg5_2.jpg)

Many software engineering textbooks suggest using the following to create the singleton utilizing the heap as shown in Figure \ref{fig:modifiedSingleton}.

![Modified controlled singleton creation \label{fig:modifiedSingleton}](https://learning.oreilly.com/library/view/game-engine-architecture/9781466560017/images/ilg5_3.jpg)

This still does not give us a way to control the destruction order though. That is a problem because what if a manager that is dependent on another manager is released back to memory before itself. For example `RenderManager` is dependent on `TextureManager`, if `TextureManager` is released first, `RenderManager` may try to call `TextureManager` which would result in a crash.

### A Simple Approach That Works
The simplest to control destruction of these singletons is to ignore the constructors and destructors and create our own that will be manually called as shown in Figure \ref{fig:bruteControlled}.

![Brute force method of creating and destroying singletons in C++ \label{fig:bruteControlled}](https://learning.oreilly.com/library/view/game-engine-architecture/9781466560017/images/ilg5_4a.jpg)

A full example is shown below in Figure \ref{fig:bruteExample}.

![A full example of using the brute method to start and stop singletons \label{fig:bruteExample}](https://learning.oreilly.com/library/view/game-engine-architecture/9781466560017/images/ilg5_4b.jpg)
