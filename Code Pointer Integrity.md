- Code-pointer integrity guarantees the integrity of all code pointer of a program (e.g., function pointers, saved return address on the stack). With CPI, all [[Control-flow Hijacking]] attacks can be prevented.

- The motivation for CPI is based on the assumption that [[Control-flow Integrity (CFI)]] is insufficient to prevent some attacks, while memory safety instrumentations have high overheads.

- One other benefit is that it selectively protect only code pointers, which is only a small fraction of pointers in a program.


- The paper introduce the notion on /sensitive pointers/, which are
1. code pointers (obviously)
2. data pointers that might access the sensitive pointers
- Determining the precise set of sensitive pointers can only be done at runtime , because of universal pointers (pointer of void* can both be code and data
pointers)

- The sensitive pointers are gotten through static type-based analysis. That is, a pointer is sensitive if it's type is sensitive. Sensitive types are code pointers, pointers to sensitive types and pointers to struct that have sensitve type as the member, and universal pointers (void* or char*).

- This analysis over-approximate the sensitive pointers, as some void* pointer may never become code pointers in the program execution.

- To enforce CPI, the original authors split the memory space into *safe region* and *regular region.*

+ The safe region is protected by allocating the region in a random location, and use the segment register to store the base the safe region. 
+ Memory isolation  could be used to protect the safe region 

The program is instrumented to:
1. Place the sensitive pointers inside the safe region. Two copy is created, one original pointer and one stored in the safe region. This is to preserve compatibility, and also handle universal pointers (could be either sensitive or non-sensitive). 1. The address of the sensitive pointer (not the pointer itself), is mapped to the medata.
2. Create and propagate (through pointer arithmetic) the metadata for the
   pointers at runtime (consists of the actual value, the bounds information and
   the temporal ID (maybe for temporal safety?)). The metdata is similar to Softbound
   . Storing the actual value allows for checking the integrity of the pointer. The bounds information & temporal ID guarantee memory safety of those pointers
   1. CPI can either store the sensitive pointer in both safe and regular
      region, and check the value upon use. This can detect all control flow
      hijacking attacks.
   2. or not use the pointer in the regular region at all, and only use pointer
      in the safe region
3. Check the metadata on the dereference of such pointer.



- The key difference with [[Control Flow Integrity]] is that CPI protect the data itself (code pointers), while CFI only guarantee that the control flow transfer to the correct targets.
