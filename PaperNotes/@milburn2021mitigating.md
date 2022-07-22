---
title: Mitigating Information Leakage Vulnerabilities with Type-based Data Isolation
authors: Alyssa Milburn, Erik vander Kouwe, Cristiano Giuffrida
year: 2021
published: [[]]
conference: 
---

The paper proposed the use of [[Pointer Masking]] for isolating data. One  key differences with previous [[Data Isolation]] is that data is   isolated based on their *type*, which removes the need for manual annotation or pointer analysis.


Pointer masking scheme [[Software Fault Isolation]], but the instrumentation is performed on *pointer arithmetic*, in stead of load and store instructions.

In overview, the type-based allocator allocate object into *arenas* 
of 4GB, identified by a pointer upper 32-bits. 4GB guard zones are inserted before and after the arena. The masking contain the pointer arithmetic such that it always generate new pointers that points to the contained arena or the guard zone.


The paper proposed many static analysis to reduce the number of instrumentation. Static analysis supports the detection of pointers that would fall within the arena / guard zone.
One key design is the *categorization* of pointer arithmetics:
- Valid pointers are returned by malloc, in the argument and loaded from memory. Valid pointers is guaranteed to be within the arena, so the upper 32 bits are correct
- Safe pointers might points to the guard zone, so dereferencing them could cause page fault.
- Unsafe pointers that would be use in a loads must be masked.

The key observations from analysis:
- In a loop, if the previous loop iteration is valid, and the loop increment is < 4GB, the current iteration would also be valid.
- Value used in load/store are always pointers, so backward/forward data flow analysis could be done to 
- When pointer dereference is successful, a safe pointer turns into valid pointer, because it would be fault if not. They call this *dominating pointer accesses*.
- Using 32-bit xor would explicitly clear the upper bits, which reduce the number of instructions





