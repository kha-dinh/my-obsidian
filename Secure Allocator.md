- [[Memory Quarantine]]-based defenses prevent the reuse of the memory region used for an object after it as been freed. 
- [[Randomized Allocations]] randomize the addresses of each allocated object, making it harder to exploit use-after-free
- Implicit [[Pointer Invalidation]] also modify the allocator