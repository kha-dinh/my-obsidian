---
alias: CHERI
title: The CHERI capability model: Revisiting RISC in an age of risk
authors: Jonathan Woodruff, Robert N. M. Watson, David Chisnall, Simon W. Moore, Jonathan Anderson, Brooks Davis, Ben Laurie, Peter G. Neumann, Robert Norton, Michael Roe
year: 2014
---


- Enforce memory capabilities in RISC: 
	- A pointer also represents access rights to a memory range, is unforgable.
	- All memory accesses must be through the memory capabilities (stored in a register), with the capability instruction.
- Tagged memory is used in conjunction to protect the capability tokens from manipulation [[Implementation of Capability-based Security#Protecting the capability token]]
	- A tag bit tag memory locations that are used to store capabilities. When non-capability instruction store to the memory, the bit is cleared.
	- Force that capabilities manipulation must always *reduce* the privilege of a token. This makes the token unforgable.
	- This also remove the need for kernel intervention, which is slow.
	
# Use cases	
## Memory Safety
- With pointer capability, pointer dereferences can be guaranteed to be to the intended location. 
## Sandboxing


