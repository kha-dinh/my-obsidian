---
title: The Taming of the Stack: Isolating Stack Data from Memory Errors
authors: Kaiming Huang, Yongzhe Huang, Mathias Payer, Zhiyun Qian, Jack Sampson, Gang Tan, Trent Jaeger
year: 
---
- The [[Multi-stack Defense]] approach is used, but with extensions to temporal & type safety
- The paper provides a unified perspective on protecting stack against memory  corruption errors, combining the works that provide [[Temporal Safety]], [[Spatial Safety]] and [[Type Safety]].

- The main contribution of the paper is to precisely and safely identify the maximal set of *safe* objects (minimal set of *unsafe* objects). This reduces runtime checks and increase the security.

- Safe objects are *filtered* in passes, each pass narrow narrow down the set of unsafe objects: 
	- The first pass classify the type of unsafe objects, using previous methods (CCCure, SafeCode)
	- The second pass create *Safety Constraints*, constraints in which if satisfied, the object can be mark as safe. Any object that fail to generate constraints are unsafe.
	- Third step *validate* the constraints of the objects. 
		- First, [[Static Analysis]] is used to validate the constraints
		- Second, if static analysis cannot validate, [[Symbolic Execution]] is employed to validate the constraints
		
- The result are more precise and faster than Safe Stack on SPEC CPU2006 (11.3% to 4.3%)