- [[Pointer Tagging for Garbage Collection]]
- [[Least-privileged functions]]
- [[Automatic PIM Offloading]]

# Research questions
## Compartment policies
- [[@clements2018aces]] introduce an algorithm that determine the compartments based on the data dependencies. To reduce the number of partitions, an ad-hoc merging strategy is used, where you could either merge data nodes or function nodes. Is there a sound & quantitative way to compartment programs?



## Profile-guided Compartmentalization
We observe that the challenges of guaranteeing least-privilege in modern software  lies in the complexity of heap memory memory acceses. Heap object allocation and their usage might belong to different functions, which makes statically analyzing them



PGComp use dynamic profiling to collect memory accesses of the functions within, and matches them to the allocation site. 

From the profiling information, it builds a graph


One challenge is that heap objects are dynamically allocated and freed. This means that a function might access  

Due to the dynamic nature of heap objects, it is difficult to track their life cycle.





