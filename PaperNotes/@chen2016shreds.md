---
title: Shreds: Fine-Grained Execution Units with Private Memory
authors: Yaohui Chen, Sebassujeen Reymondjohnson, Zhichuang Sun, Long Lu
year: 2016
---

- The paper introduce a new primitive for [[Intra Process Isolation]], called the *shred* (Segmented Threads). 
- The shreds are fine-grained isolation unit (smaller than a thread) that have exclusive access to *s-pool*, a pool of memory protected by ARM memory domain.
	-  The pool is identified  with a  pool descriptor, switched to with the API call *shred_enter(pool_desc)*
	
- The shred APIs allows developer to specify isolated code. All of the API make internal call to the kernel module (*s-driver*) through ioctl. 
	- shred_enter(ID) and shred_exit: enter and exit shred 
	- spool_alloc and spool_free: allocate and free
	
- The goal is to prevent memory corruption error to leak secret inside a shred to attackers. Compiler instrumentation (with *s-compiler*) is used to harden the execution of shreds.
	- Data flow from shred memory pool to normal memory must be sanitized.
	- Control-flow hijacking of in-shred execution must be prevented. 
		- Coarse-grained CFI is enforced: Only control flow transfer targets within a shred are allowed.
	- When functions are used out-shred and in-shred, they are duplicated. The one used in-shred is instrumented.
- Each shred also use a separated stack allocated inside the s-pool. 
- Multiplexing of domains to overcome fixed numbers
