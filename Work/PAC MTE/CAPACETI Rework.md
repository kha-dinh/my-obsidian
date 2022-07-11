---
geometry: margin=2cm
---


# Reviewer Comments
- [[CAPACETI Review Comments]]

# Summary
| Issues                                  | Mentioned By |
| --------------------------------------- | ------------ |
| [[#Applicability]]                      | R3, R4       |
| [[#Security Evaluation & Threat Model]] | R2, R3, R4   | 
| [[#Evaluation need improvement]]        | R3, R4       |
| [[#Differences with related works]]     | R2, R3       |
| [[#Extra features]]                     | R3, R4       |

# Improvements
## Applicability 
- [[#Reviewer 3]] says applicability need to be improved
	- files_lookup_fd_raw is only available on linux >=5.11
	- What are the developer requirement (expertise, effort, time)
- [[#Reviewer 4]]: 
	- Perhaps an example use case in lighthttpd with a code snippet?
	- Only validation for a certain function?
	> Does the user get fine-grained control? For example, if the user trusts most of the code and requires validation only for a particular function or library, does the current framework allow for this kind of fine-grained access control?
	- Does the user enable CAPACETI at runtime?	
## Security Evaluation & Threat Model
- [[#Reviewer 2]] 
	- Reuse attack on ARM PAC
	+ Blind ROP attacks?
- [[#Reviewer 3]]
	- Threat model is unclear
- [[#Reviewer 4]] 
	- Claims about brute-force are flawed.
	> Brute-forcing, a 64-bit ASLR, requires 2^64 (10^18) tries, while brute-forcing CAPACETI needs only 2^16 (10^4) tries since the fd field is constant.
## Evaluation need improvement
- [[#Reviewer 3]] Overhead of `capaceti_init` on short-lived & respawning processes.
- [[#Reviewer 4]] : Only 1 benchmark is done. Should have series of benchmark.
## Differences with related works
- [[#Reviewer 2]] say difference with Capsicum and CHERI should be mentioned. 
- [[#Reviewer 3]]
	- Capsicum, seccomp, OpenBDS pledge, eBPF
	- Can CAPACETI be achieved by slightly modify the existing schemes? Why is PAC necessary here?
## Extra features
- [[#Reviewer 3]]: Interaction with Enhanced Pointer Authentication
- [[#Reviewer 4]]
	- How context switch (e.g., interrupts) are handled?
	



