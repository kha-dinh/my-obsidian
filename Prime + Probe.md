
-  The attacks first load data into the cache set (*priming*). Then, it allow the victim to execute. After, it *probe* the cache set to see if the cache set is still occupied (have not been evicted). If it is evicted, the victim has accessed the cache set.
- Have no requirement of shared memory
- To perform the attack, the *eviction set* need to be constructed. Eviction set is group of $w$ different addresses mapped to one cache set in $w$-way [[Set-associative Caches]]).