___
- The API Server is the component that exposes the APIs.    
- Every operation (whether via `kubectl` or direct REST call) goes through it.    
- It listens by default on port 6443.
#### Examples:
- Get cluster version:  
    `curl https://<api-server>:6443/version`
- Get all pods:  
    `curl https://<api-server>:6443/api/v1/pods`
___
The Kubernetes API is split into groups
- Two main groups
	- Core Group
	- Named Group
___
#### Core Group 
URL prefix: `/api/v1`
Includes resources like:
- [[Pod]]
- [[Service]]
- [[Namespaces]]    
- [[ConfigMaps]]
- [[Secrets]]
___
#### Named Groups

URL prefix: `/apis/<group>/<version>`

Examples:

|API Group|Contains Resources Like|
|---|---|
|`apps`|Deployments, ReplicaSets, StatefulSets|
|`networking.k8s.io`|NetworkPolicies|
|`batch`|Jobs, CronJobs|

___
### Resources and Verbs

Each resource supports actions called verbs:
- `get`
- `list`    
- `create` 
- `update` 
- `delete` 
- `watch`

These verbs become important when setting up [[Authorization]] rules

---

## How to View API Groups

You can view available APIs by:
1. Using CURL :
```bash
curl --cert client.crt --key client.key --cacert ca.crt https://<api-server>:6443
```
2. Using proxy:
```bash
kubectl proxy
# Then access:
curl http://localhost:8001/
```
- It uses your [[KubeConfig]] credentials automatically
___
⬅️ [[KubeConfig]] | [[Authorization]] ➡️
### References
1. https://kubernetes.io/docs/reference/using-api/#api-groups
2. https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.33/#-strong-api-groups-strong-
