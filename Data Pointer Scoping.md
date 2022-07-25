Goals: Scoping data pointers & variables.

In block-structured programming languages, every variable has a lexical scope indicating block(s) of source code that has access to such variable. The compiler then check for such variable scope at compile time. However, such information is lost when the source code is compiled into lower level languages.

HardScope [[@nyman2019hardscope]] proposed providing compiler scope information to a runtime hardware enforcement mechanism that enforce the scope. 

However, the scope of dynamically allocated pointers are hard to identify at compile time.

# Why?
We observe that scoping accessibility of data pointers can reduce the effectiveness of two types of exploit, data-only programming (DOP) and information leakage. 

All known data-only attacks violate variable scope at runtime ([[@nyman2019hardscope]]).

On the other hand, information leakage attacks  such as MeltDown read data from invalid scope, or exploit vulnerabilities to write sensitive data into invalid scope.
# How?