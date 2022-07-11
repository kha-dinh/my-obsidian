# Controlled Channel Attacks
- There are two types of controlled-channel attacks:
	- [[Interrupt-Driven SGX Attacks]] triggers precise interrupts with the APIC timer to trigger. It then performs side-channel attacks. 
	- [[Page Fault-Driven SGX Attacks]]  exploits page faults of enclaves to infers the accessed address at page-level granularity.
	
# See Also
- [[Controlled-channel Defenses]]