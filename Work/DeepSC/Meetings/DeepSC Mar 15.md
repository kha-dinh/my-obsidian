## Previous
* Find simple programs. Serverless functions?
* Clear attack model & attacker goals
* Comparison with related works 
* Why fuzzing?
* Combine with program analysis? Blind fuzzing is not useful
* Benefits over source code analysis e.g. tainting

## Simple program
* Simple classifier
    * non-ML classifier
    * https://github.com/arunnthevapalan/day-night-classifier/blob/master/classifier.ipynb
* IP resolver
* Medical risk analysis

## Attacker Model & Attacker Goal
* Attacker can collect ALL traces
* Knows the input space
* Want to infer sensitive information from trace difference
    * Control flow & Data flow leakages
	``` C
int encrypt(){
	for (bit b in key)
	    if (b)
	       mul(r, p)
	   else
	       mul(t, p)
}

 int func (int secret[3]]){
   array[secret[0]];
   array[secret[1]];
   array[secret[2]];
 }
	
	```
* From data-flow and control flow information, attacker can infer sensitive input (shown in related works)

## Related work comparison
*  Compare with one related work for each
    *  Fuzzing
    *  Trace-based
    *  Static analysis
    * Combined Symbolic execution + Trace
## Trace-based analysis vs. Static analysis for side-channel
* Trace-based is precise
* Static analysis can find where in the source code there are difference in control flow / data flow
    * Static analysis over-approximate the leakages / is inaccurate
    * False positives

## Symbolic exec vs. Fuzzing vs. Static Analysis for side-channel
* Symbolic execution may lead to path explosion
    * may not be solvable
    * may not work for large real programs
* Static analysis produce false positives
* Fuzzing comparable to those two?
    * Fuzzing is methodology and those two are techniques
    * symbolic execution and static analysis can provide information for each input

## CacheAudit - Static analysis
* Objective: automatic quantification of cache side channel
* Attack model
    * time(cache access / total execution)
    * trace(cache hit/miss)
* Measure difficulty of guessing secret input from the side channel information
    * compute upper bound of attacker’s success rate
* Input: binary
* Output: quantified side channel vulnerability
* Limitations
    * crypto-limited
	- Limitation of 

## DATA - Trace-based analysis
* Input: From program binaries + Chosen input
* Output: Where the trace difference happens.
* Limitations
    * Cannot distinguish inputs (is this a limitation?)
    * Only test on crypto libraries

## QFuzz - Fuzzing
* Attack model
    * Attacker can measure timing
    * Have input space
    * Want to infer secret input from timing difference
* Input: Java Program + Input constraints
* Output: k groups of distinguishable input
* Limitations
    * Only use timing information

## CacheD - Combined Symbolic execution + Trace
* objective: detect potential cache differences at each program point
* Methodology: symbolic execution + constraint solving
    * model cache access as symbolic formulas
    * constraint solver infer sensitive data’s effect on the cache behaviour
* Attack model
    * Attacker can observe cache access
    * want to infer secret

* Design
    * 1) get execution trace(fine-grained, dump every instruction and value)
    * 2) taint analysis; track usage of secret
    * 3) symbolic execution along the tainted inst. on the trace
    * 4) constraint solver determine leakage

* Input: cache access pattern
* Output: secret input
* Limitations
    * Bad performance(17hrs to analyse 9 crypto algorithms)
    * Requires perfect trace
    * crypto-limited


## Our - Trace-based side-channel on general programs?
* We use trace-based analysis
* Input: Program binaries + input space
* Output:
    * Where trace diff happens
    * What input causes trace diff
* Target: general programs
    * Both crypto and other applications
We show real attack that can distinguish input from input clusters.   

## Possible direction
* Combine program analysis
    * static analysis
        * control flow graph / data flow slices
    * taint analysis
    * symbolic execution

* we need to set our attack goal and methodology
    * goal: sensitive input of general program?
    * cfg/function call + DNN?
