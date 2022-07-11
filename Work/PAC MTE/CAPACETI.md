- We introduce a intra-process compartmentalization primitive called c-units.
- The c-unit are  *least-privilege* fine-grained (sub-thread) execution unit. The capabilities of c-units must be explicitly given by the developer through our API. Each c-unit is assigned a unique key for resource access right authentication. 
- Each c-unit is associated with a *protection domain*, which contains the privilege of that C-unit. 
	- Privileges includes syscall, mem access.
	-  The capability tokens are bound to a c-unit that represents its capabilities.
		- Path, FD, ptr 


```C
// Global
char* private_key;
char* plain_text;
char* shared_memory;


int arbitrary_read_with_pac(char* addr){
	check_pac(addr);
	read(addr, NULL, NULL);
	return 0;
}

void attacker_func (){
	cunit_enter(ATTACKER_DOMAIN);

	// Attack on signed path (not possible with openat)
	// char* path = cap_alloc(64); // Path is signed
	// path = "/etc/passwd"
	// cap_open(path) // Valid because path is signed

	// Control flow attacks (not possible with CFI)
	(void*)func_ptr();
	// func_encrypt();

	// Cross-cunit memory reads -> separated stack & heap
	arbitrary_read_with_pac(ptr);

	// Memory reads / write into host -> memory capability
	arbitrary_read_with_pac(host_ptr);

	syscall(); // valid
	()malicious_syscall();// doesn't work because of PAC

	
	char* ptr = cap_malloc(4096);
	// 0x(ValidAC)(1)deadbeef
	cap_free(ptr);
	arbitrary_read_with_pac(ptr);
	cunit_exit();

	cunit_exit();
}

void func_db_access (){
	cunit_enter(DB_DOMAIN);
	void* plaintext = cunit_get_cap(1);

	getpid();

	cunit_exit();
}

void func_encrypt (){
	// Guarantees:
	// - this cunit and only this cunit (no other domain) can only open etc 
	// - only this cunit can access plaintext

	cunit_enter(CRYPTO_DOMAIN);
	void* plaintext = cunit_get_cap(1);
	void* key = cap_malloc(64); // Private

	cap_openat(signed_fd, "passwd", O_READONLY);
	cap_read(key, fd, size);


	check_pac(plaintext);
	encrypt(key, plaintext, size);
	cap_free(key);
	cunit_exit();
}


// 	void* path = cunit_get_cap(2); // Signed Path
// 	int fd = cap_open(path, O_RDONLY);
// 
// Every cunit has a 
//// CAPTABLE[1] = cap_A;
//// CAPTABLE[2] = cap_B;
void init_cap(){
	cap_new_domain(CRYPTO_DOMAIN);
	cap_issue_memory(CRYPTO_DOMAIN, plaintext, SIZE, 1);
	cap_issue_memory(DB_DOMAIN, plaintext, SIZE, 1);
//	cap_issue_path(CRYPTO_DOMAIN, "/etc/passwd", 2);

	cap_issue_dir(CRYPTO_DOMAIN, "/etc", 2);

	// int fd = open("/etc");

}
void main (){
	cap_enter();
	init_cap();
	func_encrypt();
	func_db_access();

}
```
- Do every API requires system calls?

- Our APIs allows the developers to define the compartmentalization boundaries and the capabilities of protection domains.
- Our compiler passes enforce the isolation of  c-unit execution
	- CFI
	- Authorization of capability tokens	
-  Our kernel module introduce light-weight modifications to the kernel that enable secure entering and exiting c-units.






