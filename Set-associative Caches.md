-  Cache lines are associated with $S$ *sets*, each set contains  $W$ cache lines (e.g., *way*), each cache line contains $B$ bytes.
	- Trade of between directly mapped cache, which have high miss rate,
	-  and fully associated cache, which has complex logic (memory is mapped to ALL cache line)
+ Memory blocks can only be cached into a specific cache set. Address $A$ can only be cached in cache set $(A/B) \text{ mod } S$
- When a cache miss occurs (the requested address is not in the cache), the associated cache line is evicted ([[Eviction vs. Flushing]]), then the memory block is copied into the cache line.

![[Pasted image 20220224171257.png]]
