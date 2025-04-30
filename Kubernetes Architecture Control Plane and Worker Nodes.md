# Kubernetes Architecture Control Plane and Worker Nodes

- Kubernetes architecture is based on a server (Master Node) and worker (Worker Nodes) style. 
1. Master Node: The master node is responsible for managing the cluster. It includes several key components:
    - API Server: Acts as the entry point for users and other components to interact with the cluster.
    - Scheduler: Assigns pods to worker nodes based on resource availability.
    - Controller Manager: Monitors the cluster's state and performs actions to maintain the desired state.
    - etcd: Distributed key-value store that stores the cluster's configuration and state.
2. Worker Nodes: These are the machines where actual workload are running. Each worker node consists of the following components:
    
    - Kubelet: Communicates with the master node and manages containers on the node.
    - Container Runtime: Responsible for pulling and running containers, such as containerd and CRI-O.
    - Kube Proxy: Handles network routing and load balancing for services running on the node.
---
⬅️ [[Introduction to Kubernetes]] | [[How to create and manage k8s components]] ➡️
### References
1. https://kubernetes.io/docs/concepts/architecture/