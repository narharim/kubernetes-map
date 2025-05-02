- Resource Requirements tells how much CPU and memory your container needs.
- There are two parts:
	- `requests` -> Minimum needed. Scheduler uses this to find a node.
	- `limits` → Maximum allowed. Container can't use more than this.

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: mypod
spec:
  containers:
  - name: myapp
    image: nginx
    resources:
      requests:
        memory: "64Mi"
        cpu: "250m"
      limits:
        memory: "128Mi"
        cpu: "500m"
```
- This means:
     - Container needs at least 64Mi of RAM and 0.25 CPU cores
    - It can use up to 128Mi RAM and 0.5 CPU cores
---
⬅️ [[Security Context]] | [[Limit Range]] ➡️
### References
1. https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/#example-1