- Published at [[OSDI]] 2020: KSplit [[@huang2022ksplit]]
- Automating the isolation of kernel drivers is challenging due to several reasons:
	- The kernel share large data structures with drivers in a fine-grained manner, i.e., driver only access a small section of the structure.
		- The structure then need to be synchronized between the driver and the kernel
	- Kernel employ concurrently executed threads and requires complex synchronization primitives 
	- Kernel use low-level idioms that creates ambiguities