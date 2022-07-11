---
alias: HAKC
title: Preventing Kernel Hacks with HAKC
authors: Derrick McKee, Yianni Giannaris, Carolina Ortega Perez, Howard Shrobe, Mathias Payer, Hamed Okhravi, Nathan Burow
year: 
---

- The paper introduced API for compartmentalization of the kernel modules.
- The the proposed policy uses a two-level approach:
	- At the top level, there are *compartments*. Those are the highest compartmentalization granularity.
	- Each compartment contains on or more *cliques*, each cliques contains a *unique* collection of code and data.
		-  A section of code or data can only belong to a single clique. 
		- A clique can only belong to a single compartment
- Based on the two level, two types of policies can be defined:
	- The *clique access  policy*  define which cliques can be accessed from a given clique.
	- The *compartment transition policy* define the allowed control flow transfer between one compartment to another. 
	
- The policies are enforced using PAC and MTE.
	- MTE enforce the *memory isolation* between the *cliques*.
		- Each clique is assigned a unique tag.
	- PAC enforce the *ownership* of pointer to each clique. The current clique and its allowed accesses is encoded in the PAC metadata.
		-   Before the pointer is referenced, the PAC modifier (authentication token) is constructed and verified with the PAC tag.
	
- The two-level policy and the use of PAC allows for tag to be reused across different compartments.
