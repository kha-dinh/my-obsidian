
1. Identify the connection between the victim and the attacker. 
	1. Identify functions calls of a shared library
	2. Identify exploitable shared cache lines
	3. Knowing *When* the exploitable code is called can be challenging ([[@gruss2015cache]])
2. Collect the victim cache accesses leaked by the connections, using some [[Cache Attack Techniques]]
3. Infer cache behavior of the victim from the trace
4. Infer sensitive information