---
title: DynPTA: Combining Static and Dynamic Analysis for Practical Selective Data Protection
authors: Tapti Palit, Jarin Firose Moon, Fabian Monrose, Michalis Polychronakis
year: 2021
published: [[]]
conference: 
---

The paper extends on the basic idea of using  [[Points-to Analysis (Pointer Analysis)]] to identify access using pointers to the sensitive program objects. On accesses that are sensitive, the in-register data is encrypted before stored into memory, and decrypted after loaded from memory into a register. 

Points-to analysis on large programs leads to over-approximation: pointers that may points to both sensitive and non-sensitive objects must be instrumented with encryption for guaranteed soundness (no unencrypted sensitive data inside memory).

The author suggests combining  [[Dynamic Information Flow Tracking]] and [[Points-to Analysis (Pointer Analysis)]] leads to a better results. DIFT track the propagation of sensitive data throughout the program, which allow the program to determine precisely where to encrypt and decrypt.

[[Steengard Pointer Analysis]] is first performed to find potential target for DIFT. Steengard is used because it is faster than Andersen, but is more impecise. The paper then use  pointer analysis results to "scope" the DIFT to those functions. This leads to less instrumentation for DIFT.

After, the load and store instructions are instrumented so that it first check "taint" of the location. If it is tainted then encryption is performed. 
e.g., for load: `tainted(ptr)?decrypt(*ptr):ptr;`
for store: `tainted(ptr)?&*ptr = encrypt(value):ptr = value;`
