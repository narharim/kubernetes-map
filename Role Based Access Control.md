It controls who can do what in a cluster using roles and role bindings.
___
## Create a Role
It defines a set of permissions within a specific namespace.

```yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: Role
metadata:
  name: developer
  namespace: default
rules:
- apiGroups: [""]
  resources: ["pods"]
  verbs: ["get", "list", "create", "delete"]
```

___
## Create a RoleBinding

It links a user to a role in a namespace.

```yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: RoleBinding
metadata:
  name: dev-user-to-developer-binding
  namespace: default
subjects:
- kind: User
  name: dev-user
  apiGroup: rbac.authorization.k8s.io
roleRef:
  kind: Role
  name: developer
  apiGroup: rbac.authorization.k8s.io
```

___
## Scope
- Both `Role` and `RoleBinding` are namespace-scoped.
- If needed cluster-wide, use `ClusterRole` and `ClusterRoleBinding` instead.

___
## Test
- Check if a user can perform an action:
    
```bash
kubectl auth can-i create deployments
kubectl auth can-i create pods --as=dev-user
kubectl auth can-i create pods --as=dev-user --namespace=test
```
___
⬅️ [[]] | [[]] ➡️
