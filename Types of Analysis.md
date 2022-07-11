
- Pointer analysis: 
	- Points-to analysis: The memory objects that a pointer might points to 
		- Steensgaad / Unification-based: 
		- Andersen / Inclusion-based: 
		- DynPTA: Steensgaard is more scalable, but  Andersen is more accurate
		- Common problems:
			- Context-sensitivity:
				- Constantine, DynPTA: it is 
			- Heap modeling: How are heap object represented
	- Alias analysis: Do two pointers points to the same memory location?
		- May alias: two pointer may alias during execution
			- Ex: In SafeStack, safe stack objects are objects that have all of the pointers that may alias to the object memory safe
		- Must alias: two pointers must alias during execution
	- Pointer analysis is generally very expensive

- Data flow analysis/Value flow analysis:  
	- Computes potential set of value of a variable at each program points
	- Analyze if there is value-flow between two instructions.
		- E.g., an instruction that read from a memory location have a value-flow edge to another instruction that write to the same memory location
	- PtrSplit: data flow analysis can replace pointer analysis if you track the data flow of the pointer value

- Taint analysis