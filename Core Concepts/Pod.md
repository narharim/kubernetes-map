### What is a Pod in Kubernetes?
---
-   Pods are the smallest deployable units of computing that you can create and manage in Kubernetes.

### How is a Pod different from a container?
---
- A container is a lightweight package that holds an application and its dependencies, while a Pod is a group of one or more containers that are closely connected and share resources.
### Why we need a Pod in Kubernetes?
---
- The container are designed in such way that is the best practice to run only a single process per container because if you run multiple unrelated process in a single container, it becomes your responsibility to unsure that all those process are running in desired state. 
- Furthermore the unrelated process running in the same container removes the isolation benefits that comes with containerzation. if one process misbehave it can affect the other process as well.
- Thus, as you are not supposed to group multiple processes into a single container, there is need of a higher-level abstraction which is fulfilled by Pod.
### What are the benefits of running multiple containers in Pod? 
---
- Consider a scenario where the main container in a pod is a web server that serves files from
directory mounted as [[Volume]], while an additional container (a sidecar container) at regular interval downloads and store content in the web server’s directory. Thus forming a single cohesive unit of service. 

### How are containers within a Pod able to share resource and communicate with each other?
---
- When containers are created within a pod, they share the same network and UTS namespaces, meaning they all share the same hostname and network interfaces. This allows them to communicate with each other using the loopback interface (localhost). Similarly all containers of a pod share resources through storage volumes (mount namespace) and communicate through the IPC namespace.
---
### How can containers share the same IP and Port space?
- Containers in a pod run in same Network namespace, they share the same IP address and port space. This means that we cannot run the processes in containers of the same pod which has same port number or we'll run into port conflicts.
- However, Containers of different pods can run on same port, because each pod has a separate port space. 


---
⬅️ [[Container]] | [[Pod Lifecycle]] ➡️
### References
1. https://kubernetes.io/docs/concepts/workloads/pods/
2. https://www.middlewareinventory.com/blog/why-we-need-pod-in-kubernetes/