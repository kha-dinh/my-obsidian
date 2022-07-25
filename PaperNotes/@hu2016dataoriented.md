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


To identify the gadgets, 

