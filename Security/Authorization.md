- Once authenticated, a user or system (like a CI/CD pipeline) needs to be authorized
- Admins can do everything (view, create, delete)
- But other users (devs, testers) should have the limited power.
- Use cases for restrictions:
    - Developers can deploy apps, but not delete nodes.   
    - Users are restricted to their namespaces.

___
##  Authorization Mechanisms in Kubernetes

1. Node Authorization 
     - It authorizes API requests made by kubelets and grants the kubelet minimal, required privileges.  
2. Attribute-Based Access Control (ABAC)
    - User/group is linked to permissions via a JSON policy file.
    - File is passed to the API server.
    - Drawbacks:
      - Hard to maintain and requires API server restart on changes.        
3. Role-Based Access Control (RBAC)
    - Define roles (e.g., developer) with sets of permissions.
    - Assign users/groups to roles via RoleBindings [[Role Based Access Control#Create a RoleBinding]]
    - Changes to roles affect all users tied to them.
4. Webhook Authorization
    - Outsources authorization to external services like Open Policy Agent (OPA).
    - Service replies with allow/deny.
---

## Configure Authorization Modes 
- Set using the `--authorization-mode` flag on the Kube API Server
- Can list multiple modes:  
    `--authorization-mode=Node,RBAC,Webhook`
- Request is passed in order:
    - If denied, goes to next mode
    - If any mode allows, access is granted      
    - If none allow, it's denied
___
⬅️ [[]] | [[]] ➡️
### References
1. https://kubernetes.io/docs/reference/access-authn-authz/abac/
2. https://kubernetes.io/docs/reference/access-authn-authz/rbac/