## Pod Lifecycle
---
-  Prerequisite : [[Pod]]
---
### What is Pod Lifecycle?
- The lifecycle of a Pod goes through several phases
1. Pending: In this phase, the Kubernetes scheduler assigns a node to the Pod and downloads container images over the network. As one or more containers have yet to be set up, it's in pending state.
2. Running: Once the Pod has been scheduled to a node and the container(s) within it are started, it enters the running phase.
3. Succeeded: If the containers within the Pod complete their tasks successfully and terminate, the Pod enters the succeeded phase. 
4. Failed: if any container within the Pod terminates with a non-zero exit code, the Pod enters the failed phase indicating that the containers within the Pod did not complete their tasks successfully.
5. Unknown: if the Pod's status cannot be determined, it is marked as unknown. This might occur due to an issue communicating to Kubernetes API or node where the Pod should run.
#### Next we're going to see [[]]
### References
1. https://kubernetes.io/docs/concepts/workloads/pods/pod-lifecycle/