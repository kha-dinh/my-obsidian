- An approach that *tag* pointers with some metadata (preferably in the unused bits)
	- This is similar to pointer tainting?
- The program is then instrumented to use the metadata for security checks

# Detecting use-after-free
- Pointer tagging-based defenses detects [[Use-after-Free]] by instrumenting pointer dereferences to use the in-pointer metadata to verify the pointer's validity