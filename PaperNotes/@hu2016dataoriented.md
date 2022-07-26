---
title: Data-Oriented Programming: On the Expressiveness of Non-control Data Attacks
authors: Hong Hu, Shweta Shinde, Sendroiu Adrian, Zheng Leong Chua, Prateek Saxena, Zhenkai Liang
year: 2016
published: [[]]
conference: 
---

The authors extends on the feasibility of [[Data-oriented Attacks]] by introducing a technique called *Data-oriented Programming*. 

The key idea is to exploit loop structures within the program that has overflow vulnerabilities that allows the attacker  to overwrite non-control data. Such loop might contains one or more *data-oriented gadgets* that are controlled by the attacker. For example, in the following code, a buffer overflow at `readData` in line 7 might allow attacker two overwrite `type`, `size`, `srv`, `connect_limit`, on the stack.
The authors refer to such loop as the *gadget dispatcher*
![[Pasted image 20220725201701.png]]
The attacker might first overwrite `type` to select the condition execute
- line 10: dereference with controlled input
- line 12: assignment 
- line 13:  addition

Conceptually, the gadget dispatcher is a virtual CPU that execute virtual instructions. Each virtual instruction consists of the following gadgets: (1) controlled load, (2) arithmetic and (3) controlled store. The author use a selected location inside memory as virtual register to store the results of the gadget.

The author shows that the  DOP attack is Turing-complete -- it can immitate the  turing machine.
