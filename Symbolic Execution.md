- Symbolic execution is used in software testing to finds programming bugs. 
- Symbolic execution run the program *abstractly*, such that it cover all possible input of the programs.
- As opposed to [[Fuzzing]], which generates concrete inputs for the tested program, 
	- SE assign symbols to the non-constant inputs.

- For example, given the code that takes input a, b and c, 
```C
int x=0, y=0, z=0;
if(a)
	x = -2;
if (b < 5){
	if (!a && c) 
		y = 1;
	z = 2;
}
assert (x + y + z != 3);
```
- SE assign symbols to unknown inputs, i.e., $a = \alpha, b=\beta, c = \gamma$
- At each points of the program where the input is needed (e.g., branches), it explores *both* states:
	- It first chose one state (e.g., $a == \neg \alpha$), and continue on the program path
		- At the next use of input, it chose a state add the constraint (path condition) to the existing:
		- e.g., on line 5, let $\beta < 5$, constraints becomes $\neg \alpha \cap \beta < 5$
	- When states are exhausted on the program path, it chose an alternative path (e.g., $a == \alpha$)
 - The execution can be represented as a table
 | line | path condition (g)                                               | Symbolic Environment E                                         |
 | ---- | ---------------------------------------------------------------- | -------------------------------------------------------------- |
 | 1    | true                                                             | $a \gets \alpha, b \gets \beta, c \gets \gamma, x,y,z \gets 0$ |
 | 2    | $\neg \alpha$                                                    | $a \gets \alpha, b \gets \beta, c \gets \gamma, x,y,z \gets 0$ |
 | 5    | $\neg \alpha \cap \beta < 5$                                     | ...                                                            |
 | 6    | $\neg \alpha \cap \beta < 5 \cap \gamma$                         | ..., $x \gets 0, y \gets 1,z \gets 2$                          |
 | 9    | $\neg \alpha \cap \beta < 5 \cap \gamma \cap \neg(0+1+2 \neq 3)$ | ..., $x \gets 0, y \gets 1,z \gets 2$                          |
- On this path, we found that the assertion is false $(0+1+2 == 3)$, thus found an error.

 
 

# See also
- [[Fuzzing]]