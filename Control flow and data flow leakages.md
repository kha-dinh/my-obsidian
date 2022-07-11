## Control Flow Leakage
- Control flow leakage happens when there is a difference in the sequences of instructions executed that is depended on the secret.
	-  For example, the secret might be used as a branching condition that create two different control flows.
	- If attacker knows about the control flow information, the secret can be inferred
``` C
if(secret == 1)
	func_a();
else
	func_b();
```

## Data Flow Leakage
* Data flow leakages happens when the data access pattern depends on the secret.
* Attackers that can observe the data access trace (e.g., from [[Cache Attacks]]) can infer the secret value.

``` C
secret == 1;
data[secret]; // location
secret = 2;
data[secret];
```

