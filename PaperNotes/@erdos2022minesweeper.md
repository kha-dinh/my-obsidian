---
title: MineSweeper: A “Clean sweep” for drop-in use-after-free prevention
authors: Márton Erdős, Sam Ainsworth, Timothy M. Jones
year: 2022
published: [[]]
conference: 
---
![[Pasted image 20220713134753.png|300]]
The paper noted that the quarantined memory could contain pointers, until they are freed, the memory objects of pointers in-quarantine are also quarantine, leading to too much memory consumption. This also create circular references that can never be freed. For example, a heap object may store a pointer to itself, which prevent the object from being reused.

