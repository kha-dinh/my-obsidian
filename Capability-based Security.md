# In a nutshell
- Capability-based system assign a capabilities to the users.
	- In contrast [[Roled-based Access Control]] keep track of which user have  the access to which resources.
- It easier to imagine the capability as the *key* to access access a certain resource (e.g., a locked box). The key can be easily passed between different people to grant access to the same resource. 

# Benefits
- Single mechanism to provide access control to any resource: The capability token. The capability token can includes multiple access rights (in each bit, e.g., RWX).
- Capability-based system solves the problem of [[Ambience Authorities]] by requiring that the capability to access any resources must also be explicitly given to subjects.
 
# See also	
- [[Implementation of Capability-based Security]]
- [[Modern Capability-based Systems]]