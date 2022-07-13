
- The limitations are memory overheads and incomplete protection. Quarantined memory cannot be reused, which leads to more memory use. Many defenses only quarantine the memory up to N allocations, which make the protection in-complete. 
- So far it is the most practical in preventing [[Use-after-Free]].