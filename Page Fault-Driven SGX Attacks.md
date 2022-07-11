
- Exploit Page faults handling of [[SGX]] enclaves ([[SGX Page Fault Handling]]).
- The first attack [@xu2015controlledchannel] can only observe noise-free memory accesses at the page granularity.
- Different from [[Microarchitectural Side-channels]] which only extract bits of data, the attack can extract a large amount of data in a single run.
- When used in combination with fine-grained attacks such as [[SGX Cache Attacks]], it reduces noise and and increase accuracy.