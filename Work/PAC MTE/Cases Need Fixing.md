
# Zero-initialized Structs
- When a pointer is loaded from a zero-initialized struct, it would be AUT-ed and corrupt the null pointer.
- For example, the following code would fail the NULL check.
```C

typedef struct other_container {
	char* ptr;
} other_container_t;

typedef struct container {
	char* ptr_A;
	char* ptr_B;
	other_container_t other_cont; // Not pointer
	int a;
	int b;
} container_t;
...
container_t *cont = calloc(1, sizeof(*cont));
...
if(cont->ptr == NULL){
	// Do something
}
```
## Fix
1. Looks for the allocated type definition. If there is pointer members, do:
	1. Create a variable for NULL pointer.
	2.  and initialize it with a register NULL value. This will PAC the null pointer and store it into the struct. 
``` C
__attribute__((annotate("no-parts")))
void fix_ptr(void* ptr, void* loc){
	asm("xpacd %[Xd]" : [ Xd ] "+r"(ptr) : );  // prevent double PACing
    asm( "pacdza %[ptr];" "str %[ptr], [%[out]];" : : [ptr] "r" (ptr), [out] "r" (loc) : ); }

container_t *cont = calloc(1, sizeof(*cont));
fix_ptr(cont->ptr_A, &cont->ptr_A) ;
fix_ptr(cont->ptr_B, &cont->ptr_B) ;
```
2. If the struct contain member of another struct that contains pointers, the pointer also need to be initialized
``` C
fix_ptr(cont->other_cont.ptr, &cont->other_cont.ptr) ;
```
# Unpaced pointers in global  structs
- PARTS does not consider pointers in global structs. Handling them would be difficult, so we pac them manually
``` C
typedef struct string_wrap_t {
	const char* string;
	int size;
	int id;
} string_wrap_t;

static const string_wrap[] = {
	{"string1", 7, 1},
	{"string2", 7, 2},
	{"string3", 7, 3},
	{"string4", 7, 4}
}
```
## Fix
1. Check if the global value contain pointer
2. Remove `const` from the global declaration so that we can update the pointer.
3. Patch the global in a function
``` C

__attribute__((annotate("no-parts")))
int __patch_globals(){
	for (int i = 0; i < sizeof(string_wrap) / sizeof(string_wrap_t); i++))	
	{
		fix_ptr(string_wrap->string, &string_wrap->string);
	}
	// ... More global patches
	return 1;
}

```
3. Insert call to the patch function in in `main`
``` C
int main(){
	__patch_globals();
}
```


# LibC Calls
- Some libc function update a structure containing a pointer or receive a struct as an argument. We must wrap those case in a custom wrapper, and replace all uses
## Fix
- For example, `strtol` receive a `char**` pointer and update the pointer `char*`. However, the pointer is not paced in libc.
- We create wrapper that call the actual libc function.
``` C
__attribute__((annotate("no-parts")))
static int __strtol(const char* str, char** endptr, int base)
{
	char* ep;
	int ret = strtol(str, &ep, base);
	fix_ptr(ep, &ep);	
	*endptr = ep;
	return ret;
}
#define strtol __strtol
```

``` ASM
pk_get_rsapubkey
     0x000000000046e2dc <+448>:   ldur    x0, [x29, #-32]
     0x000000000046e2e0 <+452>:   autdza  x0
     0x000000000046e2e4 <+456>:   ldur    x8, [x29, #-16]
     0x000000000046e2e8 <+460>:   autdza  x8
     0x000000000046e2ec <+464>:   ldr     x9, [x8]
     0x000000000046e2f0 <+468>:   autdza  x9
     0x000000000046e2f4 <+472>:   ldr     x8, [sp, #32]
     0x000000000046e2f8 <+476>:   mov     x7, xzr
     0x000000000046e2fc <+480>:   mov     x10, xzr
     0x000000000046e300 <+484>:   mov     x1, x7
     0x000000000046e304 <+488>:   mov     x2, x10
     0x000000000046e308 <+492>:   mov     x3, x7
     0x000000000046e30c <+496>:   mov     x4, x10
     0x000000000046e310 <+500>:   mov     x5, x7
     0x000000000046e314 <+504>:   mov     x6, x10
     0x000000000046e318 <+508>:   str     x10, [sp]
  => 0x000000000046e31c <+512>:   str     x9, [sp, #8]
     0x000000000046e320 <+516>:   str     x8, [sp, #16]
```