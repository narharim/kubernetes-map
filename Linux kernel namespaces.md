# Linux kernel namespaces

## What is a namespace?
- In simple terms, namespaces are like isolated environments that isolate processes from each other.
- This provides an environment wherein the processes running inside a namespace have separate system resources like file system, CPU, memory, and more.
- Changes to the system resources inside the namespace are visible to the processes within the same namespace and are invisible to other processes running in different namespace
- Namespaces as the building foundation for **containers**.


## There are a total of 7 Linux Kernal Namespaces
 ### Mount Namespace 
 - In Linux, the file system is like a big tree with directories, and files and processes in our system share the same view of this tree.
 - Mount namespaces create separate views of the file system in an isolated environment
 - They allow processes to view the file system hierarchy uniquely.
 - They provide isolation for file system mount points. A mount point acts as an entry point for accessing the contents of the mounted file system (example: ''/" is a primary mount point for the main file system)
 ### UTS Namespace
 - UTS (UNIX Time-sharing) namespace isolates the system's hostname and domain name.
 - Hostname is a unique name given to a computer or device on a network that identifies the machine and is used to communicate with other devices.
 - This namespace allows us to run multiple containers or applications on the same host, each with its unique hostname.
 ### IPC Namespace
 - IPC(Inter-Process Communication) namespaces isolate processes to communicate within.
 - Without the namespaces, processes in different environments could unintentionally interfere with each other's communication (for example, separate shared memory segments between two processes to avoid conflicts)
 ### PID Namespace
 -  As the name suggests, PID (ProcessID) namespaces provide isolated environments where processes within different PID namespaces can have the same PIDs.
 - These allow conflicts and interference between processes in different namespaces and allow containers to suspend/resume the processes.
 - The first process created gets the number 1 while running the container. This has the same privileges and capabilities as the usual init process in a standard Linux system.
 ### Network Namespace
 - Network Namespace isolates networking components like network devices, IP tables, and firewall rules.
 - Every network interface, like Wi-Fi or Ethernet, is associated with exactly one namespace. We can move these interfaces between namespaces.
 - Each network namespace has its own set of private IP addresses, routing tables, and firewall configurations.
 ### User Namespace
 - User namespace provides isolation of user and group identities.
 - Each user namespace has its own set of user and group IDs.
 - User namespaces enable more robust isolation and security by providing an additional layer of defense against unauthorized access.
 ### Control Group Namespace
- Control Group (group) namespaces allow us to create groups within which the usage of various types of system resources can be limited, like processes, memory, and CPU.
- This allows to defines the equal share of the process running across different namespaces and preventing one process from fully exhaust the available resources
 
⬅️ [[container]] | [[Namespace APIs]] ➡️ 
### References
1. https://man7.org/linux/man-pages/man7/namespaces.7.html