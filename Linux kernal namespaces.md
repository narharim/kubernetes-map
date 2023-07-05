## Linux kernal namespaces
---
-  Prerequisite : [[container]]
---
## What is a namespace?
- In simple terms, namespaces are like isolated environments that isolate processes from each other.
- This provides a environment wherein the processes running inside a namespace has separate system resources like file system, CPU, memory and more.
- Changes to the system resources inside namespace is visible to the processes within the same namespace and are invisible to other processes running in different namespace
- Namespaces as the building foundation for **containers**.
## There are total 7 Linux Kernal Namespaces
 ### Mount Namespace 
 - In linux, the file system is like a big tree with directories and files and processes in our system share the same view of this tree.
 - Mount namespaces create separate view of the file system in an isolated environment
 - They allow processes to have their own unique view of the file system hierarchy.
 - They provides isolation for file system mount points. A mount point acts an entry point for accessing the contents of the mounted file system (example: ''/" is primary mount point for the main file system)
 ### UTS Namespace
 - UTS (UNIX Time-sharing) namespace provides isolation of the system's hostname and domain name.
 - Hostname is a unique name given to a computer or device on a network which identifies the machine and is used to communicate with other devices.
 - These namespace allows us to run multiple containers or application on the same host, each with it's own unique hostname.
 ### IPC Namespace
 - IPC(Inter Process Communication) namespaces provides isolation for processes to communicate within.
 - Without the namespaces, processes in different environments could unintentionally interfere with each other's communication (example: seperate shared memory segments between two processes to avoid conflicts)
 ### PID Namespace
 -  As the name suggest, PID (ProcessID) namespaces provides isolated environments where processes within different PID namespaces can have the same PIDs.
 - These allows conflicts and interference between processes in different namespaces and allowing containers to suspend/resume the set of processes.
 - While running the container the first process created gets the number 1. This has same privilege and capabilities as the usual init process in normal linux system.
 ### Network Namespace
 - Network Namespace provides isolation of components related to networking like network devices, ip tables, firewall rules.
 - 
 ### User Namespace
 ### Control Namespace
 
#### Next we're going to see [[]]
### References
1.