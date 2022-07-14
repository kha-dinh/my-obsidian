Use-after-free happens when an in-memory pointer whose object is already freed is dereferenced.

They are hard to detect use-after-free with [[Static Analysis]] because the point of allocation and the use might be far away. The pointers can also be copied to another locations.

# Defenses
Approaches for preventing use-after-free:
- [[Secure Allocator]]-based defenses enhance the allocator behaviors to *prevent* use-after-free at the root cause. The allocator therefore *implicitly* prevents after-free erros
	- They can be to be a *drop-in* replacement without recompilation. 
- [[Access Validation (UAF)]]-based techniques instrument the program with code to validate pointer reverences. To achieve this, they attach a unique attribute (metadata) to each allocated object. When a pointer is dereferenced, the referenced object's validity is checked. This requires instrumentation of the pointer references with *explicit checks*.