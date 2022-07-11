---
title: Klotski: Efficient Obfuscated Execution against Controlled-Channel Attacks
authors: Pan Zhang, Chengyu Song, Heng Yin, Deqing Zou, Elaine Shi, Hai Jin
year: 2020
---

- The paper argue that by preventing coarse-grained attacks such as [[Controlled-channel Attacks]], fine-grained attacks such as [[SGX Cache Attacks]] are significantly more difficult to perform.
- This is because most SGX attacks  rely on coarse-grained attacks, which have less overhead, to pin-point the target code.

+ An interesting technique is proposed that emulate the entire memory subsystem.
	+ Emulated caches (vCache) for data and code 
	- The software MMU translate logical address (put in by instrumenttation) into real virtual address  (in vCache)
		- Using a page table
	- In ORAM terms:	
		- mini-page = ORAM block
		- virtual page table = position map
	- Code & data is fetched into vCache using ORAM at *mini-page* level



	
- The paper directly improve upon [@ahmad2019obfuscuro] with:
	- Better ORAM algorithm ([[RingORAM]] vs [[PathORAM]])
	- Configurable security:
		- Small vCache size get full obfuscated execution
		+ Larger vCache size have weaker security
	- Optimizations.

	
	
	