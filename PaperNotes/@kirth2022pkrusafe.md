---
title: PKRU-safe: Automatically locking down the heap between safe and unsafe languages
authors: Paul Kirth, Mitchel Dickerson, Stephen Crane, Per Larsen, Adrian Dabrowski, David Gens, Yeoul Na, Stijn Volckaert, Michael Franz
year: 2022
published: [[]]
conference: 
---

The paper proposed an [[Compartmentalization]] framework that uses [[Intel MPK]] to isolate the unsafe libraries in [[Rust]]. Its goals is to separate the memory of trusted (T) and untrusted (U) components. 


The design is simple, the address space is partitioned into MU (untrusted memory) and MT (trusted memory).  T can access MU and MT, while U can only access MU. Stack memory and global of T is exclusive to T.  For any heap memory that is shared between T and U, it marks the memory as untrusted and allocate them in MU.

The author use source code annotation to annotate the interface between trusted code and the library. This is because instrumenting all libraries interface is a too strict policy.

A challenge is to determine memory that is used by the untrusted component. The paper used [[Dynamic Information Flow Tracking]] to determine such memory. It instrument allocation functions in T as the taint source, and the interfaces to U as the sink. It then use profile input to collect the taint, any memory that flow into U is changed to be allocated into U.

The paper proposed an interesting use case of DIFT.  Instead of tracking the information flow at runtime, the paper uses profile data to determine the potential runtime information flow, and instrument the program to be "dataflow-aware". This is different from previous papers such as [[@palit2021dynpta]] that track the data flow at runtime and enforce the isolation. The authors compare the approach with that of [[SELinux]].

However, this requires a complete profiling dataset that explore all program path, otherwise share data is not identified. The authors argue that the the same could be done with static data-flow analysis, however the analysis is both unsound (miss shared memory), over-approximate the amount untrusted data, and have to high analysis time. In general, dynamic analysis would be more practical.






