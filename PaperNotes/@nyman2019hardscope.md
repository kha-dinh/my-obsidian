---
title: HardScope: Hardening Embedded Systems Against Data-Oriented Attacks
authors: Thomas Nyman, Ghada Dessouky, Shaza Zeitouni, Aaro Lehikoinen, Andrew Paverd, N. Asokan, Ahmad-Reza Sadeghi
year: 2019
published: [[]]
conference: 
---

The paper argue that containing variable uses to its "scope" defined by the programming language (e.g., functions) would prevents [[Data-oriented Attacks]]. 

Essentially the system creates a unique domain for each function that has least privilege: the function can only access the memory regions that is within its scope indicated by the source code (local vars, global). To access memory outside of its scope, a function has to be "delegated" the capability to access such memory. 


Allocated heap object is assigned to the caller. 

# Implementation

![[Pasted image 20220725132354.png]]

The system scope the memory access of each functions to only their own local variables. The implemented this with a "storage region stack" (SRS) that keep track of which memory regions the function is allowed to access. In Figure 2, function A has x,y in the stack, and function B has i,j in the stack. Any arguments pointers must be *delegated* to the function. For instance, in Figure 2, a function C could be invoked by function A or B. When A calls C, its "delegate" x and y on its local SRS to C so that C can access them. If B has a vulnerability that allows it to send any argument to C, B cannot delegate what is not in its scope (e.g., i and j). 


