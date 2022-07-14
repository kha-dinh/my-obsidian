Is an approach that *tag* pointers with some metadata (in the unused bits). The program is then instrumented to use the metadata for security checks.

Is sometime referred to as [[Low-fat Pointers]], in contrast to [[Fat Pointers]] that extends the pointer's representation with metadata (i.e., `struct fat_ptr {uint64_t base; uint64_t bound; void* actual_ptr;}`)

The metadata naturally travels with the pointer in memory copy and pointer arithmetic, so there is no need for instrumentation for tag propagation.

# Limitations
Limitations include excessive overheads from program instrumentation. Some solves this by conservatively instrumenting only neccessary pointers (e.g., pointers that might be used for UAF ([[@farkhani2021ptauth]],[[@cho2022vik]])).

Pointers that are tagged might be incompatible with uninstrumented code, because the tag bits changes the pointer's referenced address and need to be removed or ignored before used.
- There are hardware support for pointer tagging that allows the MMU to ignore the pointer's tag [[ARM Top-byte Ignore]], [[Intel Linear Address Masking]], allows them to be compatible with uninstrumented code
- 
# Memory safety
- [[Spatial Safety with Pointer Tagging]] 
- [[Detecting UAF with Pointer Tagging]]