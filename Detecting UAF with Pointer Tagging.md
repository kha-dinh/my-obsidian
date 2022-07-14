# Detecting use-after-free
Pointer tagging-based defenses detects [[Use-after-Free]] by instrumenting pointer dereferences to use the in-pointer metadata to verify the pointer's validity

For instance, the pointer's metadata could contain the object's ID, which is use as an index to lookup for its allocation status in a table ([[@cho2022vik]]).
