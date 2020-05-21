---
title: "MicroC-OS: The Real Time Kernel"
header-includes:
	- \usepackage[a4paper, margin=0.5in]{geometry}
	- \fontfamily{qag} 
	- \renewcommand{\familydefault}{\sfdefault}
---

# Real-Time Kernel Concepts
Real-time systems are characterized by the fact that severe consequences will result if logical as well as timing correctness properties of the system are not met. There are two types of real-time systems: *soft* and *hard*. In a *soft* real-time systems, tasks are performed by the system as fast as possible, but don't have to finish by specific times. In *hard* real-time systems, tasks have to be performed not only correctly, but also in a timely fashion. This book assumes a *soft* real-time system.

Real-time software applications are typically more difficult to design than non real-time applications. The use of a real-time kernel will simplify the design process by allowing the application to be divided into multiple tasks managed by the kernel.  

## Multitasking 
Multitasking is the process of scheduling and switching the CPU between several tasks; a single CPU switches it attention between several sequential tasks. One of the most important aspects of multitasking is that it allows the application programmer to manage complexity inherit in real-time applications. Application programs are typically easier to design and maintain if multitasking is used. 

## Task
A task, also called a thread, is a simple program that thinks it has the CPU all to itself. Each task is assigned a priority, its own set of CPU registers, and its own stack area. Each task is typically an infinite loop that can be any one of six states: dormant, ready, running, delayed, waiting for an event, or interrupted. 

## Context Switch or Task Switch 
When the multitasking kernel decides to run a different task, it simply saves the current task's context (CPU registers) in the current task's context storage area. 

## Non-Preemptive Kernel
Non-Preemptive kernels require that each task does something to explicitly give up control of the CPU. Non-preemptive schedule is also called *cooperative multitasking*; tasks cooperate with each other to relinquish control of the CPU. Non-preemptive kernels are much simpler to design than preemptive kernels. One advantage of a non-preemptive kernel is that interrupt latency is typically low. Non-preemptive kernel can also make use of non-reentrant functions (at the task level). Non-reentrant function can be used by each task without fear of corruption by another task. This is because each task can run to completion before it relinquishes the CPU. Non-reentrant functions, however, should not be allowed to give up control of the CPU. 

Another advantage of non-preemptive kernels is the smaller need to guard shared data throughout the use of semaphores protecting shared variables, because each task owns the CPU without the fear of being preempted. This is not an absolute rule and in some instances, semaphores should still be used. Shared I/O devices may require the use of mutual exclusion semaphores; for example, a task might still need exclusive access to a printer. 

The only way a task can be preempted is from an interrupt; an *Interrupt Service Routine* (ISR) always has priority over a task. The ISR always returns to the interrupted task. The most important drawback of a non-preemptive kernel is responsiveness. A higher priority task that has been made ready to run may have to wait a long time to run, because the current task must give up the CPU when it is ready to do so. Most real-time kernels are preemptive because of this possible delay. Non-preemptive kernels are non-deterministic; you never really know when the highest priority task will get control of the CPU. 

## Preemptive Kernels
µC/OS is a preemptive kernel. A preemptive kernel is used when system responsiveness is important. The highest priority task ready to run is always given control of the CPU. 

With a preemptive kernel, execution of the highest priority task is deterministic; you can determine *when* the highest priority task will get control of the CPU. 

Preemptive kernels should not make use of non-reentrant functions unless exclusive access is ensured though the use of mutual exclusion semaphores, because both a low priority task and high priority task can make use of a common function. Corruption may occur if the higher priority task preempts a lower priority task which is making use of the function.

## Reentrancey
A reentrant function is a function that can be used by more than one task without the fear of corruption. A reentrant function can be interupted at any time and resume at a later time without loss of data. Reentrant functions either use local variables (i.e. CPU registers or variables on the stack) or protect data when global variables are used. 

## Static/Dynamic Priority
Task priorities are said to be *static* when the priority of each task does not change during the application's execution. Each task is thus given a fixed priority at compile time.  

It is said to be dynamic if the priority of the task can be changed during runtime. µC/OS allows task priorities to be changed dynamically.


