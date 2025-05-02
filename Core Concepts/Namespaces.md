
---
- Namespaces groups resources to provide isolation between them.
- Its a way to divide cluster resources between multiple users (via [[Resource Quotas]])
- It can be used for separating resources between projects or applying quotas. 
- Resource names must be unique within a namespace but can be duplicated across namespaces.
```yaml
apiVersion: v1
kind: Namespace
metadata: 
  name: dev
```
- Create resources in namespace by specify it in metadata field
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: server
  namespace: dev #Create Pod in dev namespace
  labels:
    app: webserver
    env: prod
spec:
    containers:
      - name: nginx
        image: nginx
```


## Types of Namespaces

1. default: by default creates resources in this namespace when no namespace is specified
2. kube-system: reserved for Kubernetes system components
3. kube-public: used for cluster-wide public resources
4. kube-node-lease: Holds node lease objects for node heartbeats

## Commands
1. create namespace without YAML (imperative command)
>`kubectl create namespace <name>`
2. create namespace with YAML (declarative command)
> `kubectl create -f namespace-definition.yaml`
3. set context for namespace
> `kubectl config set-context $(kubectl config current-context) --namespace=dev`

### Related
- [[Linux kernel namespaces]]

⬅️ [[Namespaces]] | [[]] ➡️
### References
1. https://kubernetes.io/docs/concepts/overview/working-with-objects/namespaces/