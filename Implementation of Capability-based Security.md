
## Type of Access Right
- *Memory capability*: in CHERI a pointer represents the capability to access a linear range of address space [[@woodruff2014cheri]]
- *Access to system resources*:  Capsicum use the file descriptors to represents the rights to read/write files, or to call some system calls [[@watson2010capsicum]]
## Representing Capabilities
- *Capability List*: A list of (object ID, access rights) is stored for each user in protected memory (see [[#Protecting the capability token]]).  
	- a.k.a c-list
	- This is commonly used to implement implicit capabilities ([[#Implicit vs Explicit Capabilities]]) in kernels
	- When a resource is requested, the kernel check the user's capabilities in the c-list
- *Capability Token*: An unforgable token represents the access right is kept by the user
## Implicit vs Explicit Capabilities
- *Explicit capability* requires each use of the resource to present a capability token (or handle). For example, to write to a file,

- *Implicit capability* is enforced invisibly to the users. For example, the kernel store a capability list for each processes, and automatically check for processes' capabilities upon receiving a request. This approach is slower for large capability lists, but is easier to use for the users.

## Protecting the capability token
- The implementations of capability-based systems must protect the capability token from being modified by unauthorized users. Otherwise users can changes their own capabilities.  
- There are two ways to protect the keys:
	- *Using a protected storage*:  The capability can be stored inside protected storage to prevent tampering.
		+ In operating system implementations with [[Capability List]], the capabilities list is stored inside kernel memory to prevent 
		 + In hardware-enforced implementations the capabilities can be stored in read-only memories or protected registers [[@woodruff2014cheri|CHERI]].
		 
	 - *Provide only access to the index*: Capabilities can be stored in protected storage, and the index is given to the user. 
		 - [[File Descriptor]] is an example (see [[#Implicit vs Explicit Capabilities]]).
	 - *Crypto-protected Capabilities*
		 - This approach use [[HMAC]] to detect tampering in the capability token.
		 - Useful in distributed systems

