- A register is live at a points in a program where the content is used before the register is reset (by another assignment).
- The live-in registers of an instructions are the registers that are live up to the instruction
- The live-out registers of an instructions are the registers that are live after the execution of the instruction
For example
```asm
L0 : lim z, 0 
L1 : jmp L6
// live: {}
L2 : sub x, x, y 
// live: {z, x, y}
// dead: {t}
L3 : mov t, z 
// live: {z, x}
L4 : lim z, 0
// live: {t, x}
L5 : addi z, t, 1
// live: {x}
L6 : blth y, x, L2
// live: {}
```
- How  to integrate with existing automation
- Completeness of isolation
	- (Cite ERIM / similar works)
	- Data-only attacks
	- Libraries