# Runtime API
| API                              | Description                                                                | Used kmod func                   |
| -------------------------------- | -------------------------------------------------------------------------- | -------------------------------- |
| capaciti_init()                  | enable capaciti for current process                                        | initialize()                     |
| capacity_create(domID)           | set current domain to domID                                                | generate_pac_key(), new_domain() |
| capaciti_enter(domID)            | set current domain to domID                                                | switch_domain()                  |
| capaciti_exit()                  |                                                                            | exit_domain()                    |
| capaciti_issue_path(domID, path) | issue a signed path to the domain                                          | sign_path                        |
| capaciti_issue_fd(domID, fd)     | issue a signed FD to the domain                                            | sign_fd                          |
| capaciti_malloc(int size)        | allocate memory, tag with the current domain tag, sign pointer.            | -                                |
|                                  | Userspace only for performance|                                  |

# Kernel Module 
## Objects
```c
typedef struct domain_t {
	int ID;
	char* pac_db_key;	// Data  B key
	char* pac_g_key; // General Key	
	int mte_tag;
} domain_t;

// Global domain table
domain_t* domain_table;



```
- A linked list of domain_t
## API
| API                              | Description                                 |
| -------------------------------- | ------------------------------------------- |
| initialize()                     | init? allocate the domain table             |
| switch_domain(domID)             | Lookup the domain table and change PAC keys |
| pac_db_switch(new_key)           | switch                                      |
| pac_g_switch(new_key)            |                                             |
| exit_domain()                    |                                             |
| sign_fd(domID, char* path)       | Use General key                             |
| auth_fd(domID, char* path)       | Use general key. Return true if succeed     | 
| sign_path(domID, char* path)     |                                             |
| auth_path(domID, char* path)     |                                             |
| generate_pac_key()               | Generate a new PAC key                      |
| new_domain(domID, db_key, g_key) |                                             |





# Kernel Hook 
| system call    | before syscall    | after syscall | Used kmod API      |
| -------------- | ----------------- | ------------- | ------------------ |
| path-related   | authenticate path | sign the fd   | auth_path, sign_fd |
| fd-related     | authenticate fd   | -             | auth_fd            |
| memory-related | ???               | ???           |                    | 


