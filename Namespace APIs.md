## Namespace APIs
---
-  Prerequisite : [[Linux kernel namespaces]]
---
- The namespace API of the Linux kernel consist of three system calls, which allows us to create namespaces.
### clone
- When we create a new child process using the ***fork()*** system call, the child process inherits most of its attributes from the parent process. It shares the same memory, file descriptors and signal handlers.
- However when creating a new child process using the ***clone()***, the parent process has more precise control over what the parent process and child process share. It allows to place the child process in separate namespace. 
### unshare
- ***unshare()***  system call allows a process to have more control over what it shares with other processes without creating a completely new process.
- It does it by disassociating parts of its execution context that are currently being shared with other processes
### setns
- The ***setns()***  system call is used to join an existing namespaces in Linux. It allows a process to become a member of a particular namespace thereby gaining access to context and resources associated with that namespaces.
#### Next we're going to see [[]]
### References
1. https://man7.org/linux/man-pages/man2/clone.2.html
2. https://man7.org/linux/man-pages/man2/unshare.2.html
3. https://man7.org/linux/man-pages/man2/setns.2.html