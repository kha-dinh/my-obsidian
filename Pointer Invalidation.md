
# Explicit pointer invalidation
[[Dangling Pointer Nullification]] invalidate in-memory pointers to an object after it has been freed (with NULL value). 

# Implicit pointer invalidation
[[Garbage Collection (UAF)]] imitates the behavior of garbage collectors that delay the actual free of the object until there until it can be verified that there is no in-memory dangling pointers. 

# Pointer tracking
One common challenge for pointer invalidation is the accurate tracking of pointers and their propagation inside memory (a.k.a *Pointer Tracking*).

## Dynamic range analysis
[[@lee2015preventing]] instrument the program to manage a binary tree structure that stores pointer locations and the mapping to their referent at all time during the execution. At the time of pointer free, it look up the data structure to find all in-memory pointers of the object, and set them to be NULL.

## Reference counting 
[[@shin2019crcount]] uses only a bitmap to indicate memory locations containing pointers. Reference counting is used to track the in-memory references of a pointer.

## Value-based
Garbage collector algorithms commonly depends on the *value* of the pointer inside memory to invalidate them. However, in C, pointers and data are not clearly separated in-memory ([[Pointer Provenance]]).  This leads to *false positives*, since data values might match that of pointers, and prevent reusing.

There are also *false negative*, program might hide the pointers (e.g., XOR it with some value), so that the GC cannot find them during GC, and restore them later for use-after-free.

## Dynamic Taint Tracking 
[[@banerjee2020sound]] use [[Dynamic Information Flow Tracking]] to track the propagation of pointers from their allocation sites, in other words, also track the [[Pointer Provenance]].  It relies on the advances in [[Optimistic Hybrid Execution]] to reduce the overheads of dynamic taint tracking. The paper claims that pointer-provenance-based GC is sound (no false positive / detecting non-pointers as pointers), compared to other approaches.