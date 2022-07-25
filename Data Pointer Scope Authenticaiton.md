
# High level goals
The goal of this is to achieve the principle of least-privilege of pointer usage, such that pointers can only be authenticated within appropriate context.  

We use a granularity of a function. This is because the privileges of functions (its variable scopes, its input and output) are commonly well-defined in the source code. Moreover, most exploit happens at function levels. 


# Scope and assumption




# Why?
We observe that scoping accessibility of data pointers can reduce the effectiveness of two types of exploit, data-only programming (DOP) and information leakage. 

All known data-only attacks violate variable scope at runtime ([[@nyman2019hardscope]]).

On the other hand, information leakage attacks  such as MeltDown read data from invalid scope, or exploit vulnerabilities to write sensitive data into invalid scope.

# How?
We observe that for most functions, their pointer are delegated from another function.

The goal is to enforce least-privilege of function invocation.


In functions, there are 5 origins of pointers.
1. Local variables: For local variables, pointers are usually are not created from thin air, but is assign from another variables.
2. From global variables: By default, all global variables are accessible in C.
3. From dynamic allocation
4. Address of operation (with the & operator)
5. Passed from another functions as argument
6. Cast from integer to pointer (out of scope)


Explicit delegation: Parameter passing that delegate a pointer use to another function must be explicit
Complete mediation: All pointer use must be mediated for authentication. However, we saw that  this requirement could be relaxed for *safe* pointers.



Challenges:
- Delegating nested pointers.
- Revocation
- Indirect function calls
