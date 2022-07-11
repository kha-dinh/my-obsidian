Cache attack exploits attacker shared cache lines ([[CPU Caches]]) with the victim.
## Attacker's influences over the cache (thus the victim)
- Flushing the cache with CLFLUSH
- Fill the cache with its own content
- Evict the cache lines with data accesses  ([[Eviction vs. Flushing]])
	
## Leaked information
- Cache attack allow the attacker to know *when* and *where* are the memory accesses of the victim
	- The victim process might access the same cache lines or cache set ([[CPU Caches]]) as the attackers, thus create difference in the *timing*
		- Evicted cache lines takes longer to read
		- Loaded cache lines read faster
	- Based on the difference timing, the *location* of access is inferred. For example, the address of function accessed.
- [[Control flow and data flow leakages]] are inferred from the location of access

## See also	
+ [[Recipe for a Cache Attack]]
+ [[Cache Attack Techniques]]
- Most cache attacks requires manually locating the exploitable code and data in the binary.  [[@gruss2015cache]] is an automated cache attack.