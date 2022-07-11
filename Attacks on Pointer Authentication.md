# Cryptographic attacks
- Attackers might brute force the value of the PAC
- Cryptanalysis on known values
# Maliciously craft the PAC-ed pointer
- Attackers can jump to different locations that use PAC instructions to build the PAC-ed pointers
	- *Creating another PAC pointer with the same modifier*. The PAC modifier are not necessarily unique, or confidential (e.g., the Stack Pointer). 
	- *Control the modifier value*.
	- Both
- Hence, PA-based protection must also have [[Control Flow Integrity]]
# PAC Reuse
- PAC-ed pointers can be reused
	- *Rollback*: 
	- *Substitute*: Use the valid PAC from another location (e.g., with the same SP)
# References
- [@liljestrand2019pac]