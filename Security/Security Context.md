
___
- Security context is like setting security rules for your [[Pod]] or [[Container]]. 
- It defines what Pod/Container can do and cannot do inside a node.
- Container can override security context configured at Pod level
- For example:
	- Can it run as `root`?    
	- Which user/group ID should it run as?
	- What file permissions should it have?
___
## Security Context at Pod Level

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: mypod
  labels:
    env: sbox  
spec:
  securityContext:
	runAsUser: 1000
  containers:
  - image: nginx
    name: mypod
```
___
## Security Context at Container Level
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: mypod
  labels:
    env: sbox
spec:
  containers:
  - image: nginx
    name: mypod
    securityContext:
	   runAsUser: 1000
	   capabilities:
		  add: ["NET_RAW"]
```

___
⬅️ [[Secrets]] | [[Resource Requirement]] ➡️
### References
1. https://kubernetes.io/docs/tasks/configure-pod-container/security-context/