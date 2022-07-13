Garbage collectors (GC) in C aim to prevent [[Use-after-Free]] by invalidating in-memory pointers.

GC tends to be slow because of memory scanning, so many perform the scanning task periodically ([[@erdos2022minesweeper]])
# Common approaches
## Mark-and-Sweep
[[Mark-and-Sweep]]


## Pointer provenance
[[Pointer Provenance]]-based GCs ([[@banerjee2020sound]]) use [[Taint Tracking]] to track the propagation of pointers from their allocation sites. 

[[@banerjee2020sound]] claims that pointer-provenance-based GC is sound (no false positive / detecting non-pointers as pointers)
# Challenges of garbage collectors
## Detecting in-memory pointers
Garbage collector algorithms commonly depends on the *value* of the pointer inside memory to invalidate them. However, in C, pointers and data are not clearly separated in-memory ([[Pointer Provenance]]).  This leads to *false positives*, since data values might match that of pointers, and prevent reusing.

There are also *false negative*, program might hide the pointers (e.g., XOR it with some value), so that the GC cannot find them during GC, and restore them later for use-after-free.