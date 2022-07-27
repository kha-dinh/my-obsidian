# Sanitizer vs. Exploit mitigation
Exploit mitigation techniques aim to prevent / detect attacks, while sanitizers aim to pinpoint  the location of bugs. For example, [[Control Flow Integrity]] policies are exploit mitigation, because control flow hijacking is the  consequence of memory errors, not the cause. Bounds checking, on the other hand, is sanitizer.

Compared to sanitizer, exploit mitigation must have constraints because they are deployed at runtime.
- They must have low overhead
- False positive is not acceptable because they crash the program. 
- Benign errors are allowed in exploit mitigation technique for better reliability

# Reference
- [[@song2019sok]]