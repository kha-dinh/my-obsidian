



# Pointer Authentication with Points-to Info
1. Track all points-to set of pointers,
	1. A points-to target of a pointer is a memory object (allocated by malloc) that the pointer might be used to access
	2. Points-to information is propagated through [[Dynamic Information Flow Tracking]]: Let malloc site be the taint source, and propagate the taint to pointers that depends on the allocated pointer
2. At the pointer usage (load/store):
	4. Pointers that have singleton set (i.e., a single points to target) can use a unique modifier
	5. Pointers that have multiple points-to target query its points-to information in the allocation table and extract its modifier
	
##  Why?
-  

## Security 
- Given that pointers are well-defined (no out-of-bound pointers)

## Challenges
- How to propagate pointer's PAC through arithmetics
	- Pointer arithmetics update the pointer content, which also change the PAC
	- PACTight uses 



- With [[Points-to Analysis]],