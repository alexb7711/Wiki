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

### OGRE - An Example
Everything in OGRE is controlled by a singleton object `Ogre::Root`. It contains pointers to every other subsystem in OGRE and manages their creation and destruction. This makes it very easy for a programmer to start up OGRE - just a new instance of `Ogre::Root` and you're done. Examples are shown in Figures \ref{fig:ogrerooth}, \ref{fig:ogreroothpointers}, \ref{fig:ogrerootc}, and \ref{fig:ogrerootcmethods}.

![OgreRoot.h class declaration \label{fig:ogrerooth}](https://learning.oreilly.com/library/view/game-engine-architecture/9781466560017/images/ilg5_5a.jpg)

![OgreRoot.h member variables \label{fig:ogreroothpointers}](https://learning.oreilly.com/library/view/game-engine-architecture/9781466560017/images/ilg5_5b.jpg)

![OgreRoot.cpp Constructor \label{ogrerootc}](https://learning.oreilly.com/library/view/game-engine-architecture/9781466560017/images/ilg5_6a.jpg)

![OgreRoot.cpp Methods \label{ogrerootcmethods}](https://learning.oreilly.com/library/view/game-engine-architecture/9781466560017/images/ilg5_6b.jpg)

OGRE provides a template `Ogre::Singleton` base class from which all its singleton (manager) classes derive. 

## Memory Management
Memory affects performance in two ways:
1. *Dynamic memory allocation* via `malloc()` or C++'s global operator `new` is a very sow operation. We can improve the performance of our code by either avoiding dynamic allocation altogether or by making use of custom memory allocators that greatly reduce allocation cost.
2. On modern CPUs, the performance of software is often dominated by its *memory access patterns*. Data that is located in small, contiguous blocks of memory can be operated on much more efficiently by the CPU than if the same data were to be spread out accross a wide range of memory addresses.

### Optimizing Dynamic Memory Allocation
The dynamic memory allocation via `malloc()` or `new` and `delete` operators is typically very slow. The high cost can be attributed to two main factors. First, a heap allocator is a general purpose facility, so it must be written to handle any allocation size, from one byte to one gigabyte. This requires a lot of management overhead. Second, on most operating systems a call to `malloc()` or `free()` must first context-switch from user mode into kernel mode, process the request and then context-switch back to the program. These context switches can be very expensive. One rule of thumb in game development is:

>Keep heap allocations to a minimum, and never allocate from the heap within a tight loop.


