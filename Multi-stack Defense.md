- Stack objects are separated into groups of *safe* objects and potentially *unsafe* objects. Safe objects are put into a separated stack and does not have runtime protection. Unsafe objects requires runtime checks.
- This reduces the number of instrumentation in programs
- The location of the stack is protected with [[ASLR]] or [[Intra Process Isolation]] like MPK