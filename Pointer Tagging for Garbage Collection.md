Pointer invalidation is a recent ...

Recent works demonstrate that implicit pointer invalidation achieve better performance and security compared to pointer dereference validation.

Can be solve with pointer tagging.
That is, for any pointer dereferences, we can determine 

For correct pointer invalidation, previous works proposed methods for accurate *pointer tracking*, which track the pointer locations within memory.

Reference counting

Use pointer tag as 


