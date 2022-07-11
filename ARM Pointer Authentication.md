---
alias: PAC
---

- ARM PA introduce instructions to sign a given pointer with a 64-bit *modifier* (e.g., `paciasp`), and instructions to verify the *signature* (e.g., `autiasp`).
- There are 5 different keys for PAC, which are only accessible with kernel privilege

- Example use case to authenticate the return address (LR) with the stack pointer (sp) as the modifier
```asm
function : 
	paciasp; create PAC 
	stp FP, LR, [SP, #0] ;store LR 
	; ... 
	ldp FP, LR, [SP,#0] ; load LR 
	autiasp ; authenticate 
	ret ; return

```
# See Also
- [[Attacks on Pointer Authentication]]