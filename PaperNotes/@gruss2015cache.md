---
aliases: Cache Template Attack
title: Cache Template Attacks: Automating Attacks on Inclusive {Last-Level} Caches
authors: Daniel Gruss, Raphael Spreitzer, Stefan Mangard
year: 2015
---

+ Demonstrated an attack that can derive the keystroke from GTK-based and Window applications.
+ Does not assume prior knowledge (e.g., source code) about the application like other cache attacks on cryptographic functions

## Attack
- The attack consists of two phases
	- The first *profiling phase* profile the target to get the dependencies between the secret input and the cache access of the program ([[Cache Attacks]])
	+ The second phase use the information to derive the secret input from the learned observation and learned info
	
### Profiling Phase
+ The goal of this step is to create a *Template Matrix*, a matrix with the addresses as the rows, and the targeted *event* as the columns.
+ The value of the matrix is the *cache-hit ratio*: how many cache hit occur to the address over the number of time the event is triggered
+ The test repeats for *all* addresses and defined events to collect the cache-hit ratio of each address 

### Attack Phase
- The attack collect the cache-hit ratios for the events and compare it with the template matrix