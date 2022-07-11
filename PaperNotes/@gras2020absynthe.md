---
title: ABSynthe: Automatic Blackbox Side-channel Synthesis on Commodity Microarchitectures
authors: Ben Gras, Cristiano Giuffrida, Michael Kurth, Herbert Bos, Kaveh Razavi
year: 2020
---

- The system synthesize the best sequence of instruction that create contention-based side-channel.
## Analysis / Profiling Phase
+ Secret dependent control flow is identified using [[Taint Analysis]].
	+ Function with sufficient execution time is selected.
+ The program's functions are instrumented to extract the *ground truth*, which is whether the target branch is taken or not . The ground truth is sent to the attacker process through shared memory as *signals*.
	+ It is argued that using shared memory as signaling does not create noises
+ With the ground truth, the spy code take measurements (the contention-based side channel), and continue to refine the attack input (sequence of instructions that create contention & the strategies) using genetic algorithm.
+  The solution is a single sequence of instructions that generate the most contention-based timing

## Attack phase
+ During attack, there is no synchronization
- Use RNN to resistant agaisnt noise
## Notes
+ The paper focus on *contention-based side-channels*. The rationale is that the are more stealthy compared to eviction-based ones (e.g., cache attacks).
+ The attacker execute on the same core as the attacker.
## Questions
+ Why SMT? SMT CPU  vs normal CPU?
## See Also
+ [[Simultaneous Multi-Threading]] enable sharing resources across threads.
- [[Contention-based Side-channel Attacks]] exploits the contention of execution ports. It replace active eviction of [[Cache Attacks]] with passive monitoring. 
- [[@gruss2015cache]] have an automated cache attack