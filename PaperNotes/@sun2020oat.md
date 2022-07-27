---
title: OAT: Attesting Operation Integrity of Embedded Devices
authors: Zhichuang Sun, Bo Feng, Long Lu, Somesh Jha
year: 2020
published: [[]]
conference: 
---

The paper introduce a system for attesting [[Control Flow Integrity]] and detecting [[Data-oriented Attacks]] of bare-metal devices. The paper refer to this as *Operation Execution Integrity*.

It instrument the program to record the *measurement* at runtime. Measurement include  control flow information (indirect calls, branch and backward edge), and integrity of critical variables to prevent data-only attacks. The *measurement engine* is protected in [[TrustZone]].

One of the observation is that embedded programs is usually scoped to operations. Hence, the paper allow the attestation of each operation (e.g., moving a robot hand), so the scope of attestation is small.

Different from pure hash-based control flow attestation and pure trace-based, the paper use a *hybrid* control flow logging. For the indirect call, the target address is recorded (similar to trace-based CFI). For branch, 0 (not taken) or 1 (taken) is record. For return address, the chain of hash of return value is taken ($H = Hash(H_{prev} + RetAddr)$). The hybrid logging reduce the log size, while also allow control flow to be rebuilt.

To verify the control flow, the paper uses *Abstract execution*, which only emulate the effect of control flow transfers. It travel the control flow graph on direct calls. When it reaches indirect calls or branch, it pop the value from the log to select the correct control flow target. During the execution, the hash chain of return value is calculated, so that when the operation finish, the hash value must be identical to the one in the measurement. Control flow violation is detected when (1) Control flow target is not defined in the CFG or (2) hash value of backward-edge does not match.


The paper claims that detecting the corruption of *critical values* (control-dependent variables, or user-defined sensitive variables) between their *define* and *use* could detect data-only attacks.  If fine all the define (store) and use (load) of those variables, and instrument them to (1) record the last defined value, and (2) check if the value match on use.  Conceptually, this is very similar to [[@ismail2021vip]].

Using the scheme, all of the dependent value (dataflow) and usage of pointer to the value also need to be instrumented. For dependent values, it use the [[Program Dependence Graph]] and collect the dependencies of the initial critical values.  For pointers, it uses [[Andersen's Pointer Analysis]] to find the points-to set of pointers. The imprecision is not mentioned, but maybe embedded programs are small so it is not a problem.



