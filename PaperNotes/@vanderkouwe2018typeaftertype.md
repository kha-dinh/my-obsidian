---
title: Type-After-Type: Practical and Complete Type-Safe Memory Reuse
authors: Erik vander Kouwe, Taddeus Kroes, Chris Ouwehand, Herbert Bos, Cristiano Giuffrida
year: 2018
published: [[]]
conference: 
---

Proposed a [[Type Safety]] for safe memory reuse. In particular, it divide the memory allocation into pools of different types. It determine the data type at each allocation sites, and use a separate pool for that type.

One of the strait forward analysis is to perform forward analysis to find  how the returned value from malloc is casted. It also propagate the analysis to function arguments and return value to check if there is conflicting types.

The type information provided by `sizeof(type)` is useful in determining the allocation type, but is removed in the compiler pipeline. Hence the author insert a pass to preserve such information to later passes.

Inlining allocation wrappers allows malloc to be at the caller site, which simplify analysis.

A 64-bit hash is computed based on the type information. The hash is pass into the allocation library to determine which pool should be allocated. The author argue that this approach does not require runtime analysis like previous approaches.

Type that are unable to be determine at runtime uses the call site hash as the input for the allocator. This means that if the call site is used to allocate different types, the guarantees are broken.
