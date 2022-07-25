

Type safety is another approach for [[Temporal Safety]] that only allow memory reuse of the same type.

This is because a common exploit pattern is that the attacker stores pointer in a memory that is not pointer type. Then, when [[Temporal Safety]] is violated, that memory is interpreted as a pointer type and allows the pointer to be used. Similarly, when pointer are leaked  to bypass ASLR, it must bypass type safety to store pointers into data regions [[@vanderkouwe2018typeaftertype]].
