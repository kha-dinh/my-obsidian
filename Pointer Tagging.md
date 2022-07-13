- An approach that *tag* pointers with some metadata (preferably in the unused bits)
	- This is similar to pointer tainting?
- The program is then instrumented to use the metadata for security checks
- Limitations include excessive overheads from program instrumentation. Some solves this by conservatively instrumenting pointer uses that might be use-after-free ([[@farkhani2021ptauth]]).
- The metadata naturally travels with the pointer in memory copy and pointer arithmetic. IFor instance, the pointer's metadata could contain the object's ID, which is use as an index to lookup for its allocation status in a table ([[@cho2022vik]],[[@farkhani2021ptauth]]).

# Detecting use-after-free
- Pointer tagging-based defenses detects [[Use-after-Free]] by instrumenting pointer dereferences to use the in-pointer metadata to verify the pointer's validity
