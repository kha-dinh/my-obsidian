- Use-after-free happens when an in-memory pointer whose object is already freed is dereferenced.
- It is hard to detect use-after-free with [[Static Analysis]] because the point of allocation and the use might be far away. 
- The pointers can also be copied to another locations.
# Defenses
- There are generally approaches for preventing use-after-free:
	- [[Memory Quarantine]]-based defenses prevent the reuse of the memory region used for an object after it as been freed. 
	- [[Randomized Allocations]] randomize the addresses of each allocated object, making it harder to exploit use-after-free
	- [[Pointer Invalidation]] invalidates pointers when they are freed. There can be two schemes:
		-  Implicit pointer invalidation ([[Garbage Collection (UAF)]]) delay the freeing of object only if there is no more references to it.
		- Explicit pointer invalidation ([[Dangling Pointer Nullification]]) explicitly find all references of the pointer and invalidate them
	- [[Access Validation (UAF)]]-based techniques instrument the program with code to validate pointer reverences. To achieve this, they attach a unique attribute (metadata) to each allocated object. When a pointer is dereferenced, the referenced object's validity is checked. 
		- [[Pointer Tagging]]-based defense tag pointers with metadata at the allocation (e.g., in to unused bytes). Then, the program is instrumented memory dereferences to validate the pointer's metadata. 
	
- [[Garbage Collection (UAF)]] and [[Memory Quarantine]]-based defenses only changes the behavior of the memory allocator and does not requires change to the program semantics. On the other hand, [[Pointer Tagging]]-based defenses requires program instrumentation.