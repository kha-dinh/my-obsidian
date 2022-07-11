

# Object Capabilities 
## Threat model
- The original program is benign, but might contains errors that allows the attackers to perform random read/write to memory.
- Objects are memory objects (e.g., structs, buffers) or system resources (e.g., file descriptor)
- Objects belong to *groups*, identified by the memory tag.

## Capability-based Compartments
- A compartment is a subgraph of the CFG
- The code in a compartment is allowed N capabilities.
	- E.g., write access to memory with tag $T$ 
	- Perform system calls $S$ with 
- On exit, all capabilities are revoked
- Difference with HAKC?



# References
- [[@mckeepreventing|HAKC]] also used PAC & MTE
- [[@woodruff2014cheri|CHERI]] enforce pointer capability
- [[ARM Pointer Authentication|PAC]]