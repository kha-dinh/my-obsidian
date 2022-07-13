- Frequency smoothing is proposed as an alternative to [[Oblivious RAM]].
	- In ORAM, a sequence of accesses (Op,Addr,Data) with a certain distribution is transformed into uniformly distributed accesses to the ORAM tree.
		- For example, [[PathORAM]] read data blocks on the entire path the ORAM tree at a time, and update data along the read path 
	- Frequency smoothing instead does not transform the original accesses and opportunistically inject *fake accesses* into the sequence of accesses to make them seem uniform. 