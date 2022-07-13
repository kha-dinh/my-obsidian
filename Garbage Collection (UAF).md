Garbage collectors (GC) in C prevents [[Use-after-Free]] by guaranteeing that the memory object can only be freed if there is no more references (pointers) to the object.

GC tends to be slow because of memory scanning, so many perform the scanning task periodically ([[@erdos2022minesweeper]])

# Common approaches
## Mark-and-Sweep
One of the the challenges for garbage collection is to determine which quarantined objects is safe to free.

The  approach uses two phases for garbage collection: 
- The *marking* phase finds all *live* (un-freed) objects that are *reachable* from the set of *root pointers* (i.e., pointers currently on the stack, registers and global pointers).
- The *sweeping* phase free all


