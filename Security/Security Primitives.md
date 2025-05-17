___
## Security Layers
### Host-Level Security (Infra)
- Disable root login and password authentication
- Use only SSH key-based authentication
- Secure the underlying machines
- If your nodes are compromised, the whole cluster is compromised.
___
### Kubernetes API Server Access
You use `kubectl` or API clients to talk to it. So, it’s the first line of defense.

#### Two Key Questions:
- Who can access the API server? → Authentication 
- What can they do once inside? → Authorization
___
### Authentication Methods
These control _who_ can access the cluster:
- Client certificates
- External auth (e.g., LDAP, OIDC)
- [[Service Accounts]] (for apps running in the cluster)

___
### Authorization Methods
These control _what actions_ a user or service can perform:
- RBAC (Role-Based Access Control) → Most widely used
- ABAC (Attribute-Based Access Control)

___
### Securing Component Communication

Kubernetes components (like `kubelet`, `controller-manager`, `scheduler`, etc.) talk to each other using TLS encryption.
___
###  Pod-to-Pod Communication
- By default, any [[Pod]] can talk to any other pod in the cluster.    
- Use [[Network Policies]] to restrict traffic between pods.    
___
⬅️ [[]] | [[]] ➡️
### References
1.