---
title: ACES: Automatic Compartments for Embedded Systems
authors: Abraham A. Clements, Naif Saleh Almakhdhub, Saurabh Bagchi, Mathias Payer
year: 2018
published: [[]]
conference: 
---

Designed an automatic compartment system for bare metal code on [[ARM Cortex-M]]. The paper uses static analysis with LLVM and the [[Program Dependence Graph]] to partition the bare metal code into several compartments.  The memory isolation between compartments is enforced with the [[Memory Protection Unit]].

The author use a *Region graph*, a graph built on top of the PDG that split the program into regions for code (functions), data (global variables) and peripheral devices. 

![[Pasted image 20220727132522.png]]

The initial region graph is built from the PDG: each function, global and peripheral device is a node. The edge is the dependency of the function to peripheral/data nodes. All data node has a separeted region. Each code node (one or more function), along with all of its dependencies becomes a compartment. So, the outer degree of a code node must be lower than the available regions. 

The author simplify the region graph to fit into 8 regions restriction by merging nodes into one region. If two data nodes are merged, the functions that are dependent on the node are also merged. If two code nodes are merged, all of its dependencies are merged.
The user is allowed to chose merging policy.



Cross-compartment function call sites are attached with the metadata containing allowed target. Cross-compartment  call is instrumented with compartment switch that call the MPU config routine. It store the current config into an MPU stack, then load the new MPU config. The MPU configs for each compartments are protected in the read-only memory.

When the program transition into a new compartment, the previous stack is protected by a region, so the new compartment cannot access the stack before it. One challenge is to selectively allow access to the previous stack when there is data dependency. The author build a *whitelist* by running the program and catch the faulting address. Then, during runtime, the fault handler compare the access with the whitelist and *emulate* the access.



