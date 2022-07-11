- PACTight constructs the PAC using the pointer's address (&p)  and a random tag stored in shadow memory (tag(p)) as the modifier. The pointer's address prevent it from being used at other locations (non-copyability). The random tag prevent reusing the pointers that are freed (non-dangling). 
	- Runtime library provide functions to manipulate the tag, sign/authenticate pointers.
	- Especially, there is `new_p = pct_auth(&p,p+N)` that check if the created pointer is in the bound of the object, then propagate the PAC to the newly created pointers. 
- PACSafe uses shadow memory to store the ID of object allocations. It construct the PAC on the object ID, then put the PAC into the pointer's address. When the pointer is used, it look for the object ID in the shadow memory, then use the PAC within the pointer to authenticate the ID. If authentication succeed, then (1) the pointer points to the correct object 
	- Probably only guarantee heap memory safety?
	