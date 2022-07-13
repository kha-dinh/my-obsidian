---
title: CRCount: Pointer Invalidation with Reference Counting to Mitigate Use-after-free in Legacy C/C++
authors: Jangseop Shin, Donghyun Kwon, Jiwon Seo, Yeongpil Cho, Yunheung Paek
year: 2019
published: [[]]
conference: 
---
A pointer bitmap indicate every locations of pointers inside memory. The bitmap is maintained by program instrumentation that insert calls to the runtime library. Moreover, the reference count of each object is stored in a *pointer-to-object* metadata map

The paper instrument store instructions to update the bitmap. `crc_store(addr, val)`  would decreases the reference count of object pointed to by `addr`, increase the reference count of object pointed to by `val`. 

