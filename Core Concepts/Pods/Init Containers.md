- In a [[Multi-Container Pods]], all containers continues to run as long as the [[Pod]] is running.
- Sometimes, you only want to run a containers once, like:
    - Pulling dependencies before the man app starts.
- For these kinds of one-time startup tasks, we use Init containers.
- If either container stops or fails, Kubelet restarts the containers based on `restartPolicy`
	- If `restartPolicy` is set to `Always` or `OnFailure`:
		- Kubelet will restart the failing init container until it succeeds. 
	- If `restartPolicy` is set to `Never`:
		-  Kubelet will not restart the failing init container and mark `Pod`  as Failed
___
## How to create
- Init containers are just like regular containers, but they are placed in a special section in the pod YAML
- Their job is to finish a task and exit successfully.    
- The main app container won’t start until all Init containers exit successfully.

```yaml
initContainers:
- name: init-myservice
  image: busybox
  command: ['sh', '-c', 'git clone ;']
```

- This runs a Git clone command before the main app starts.
___
## Multiple Init Containers
- you can define more than one init container and they run in order and one at a time.
- The next init container won’t run until the previous one finishes successfully.
- For example: 

```yaml
initContainers:
- name: init-myservice-1
  image: busybox:1.28
  command: ['sh', '-c', 'do echo Hello; sleep 2; done;']

- name: init-myservice-2
  image: busybox:1.28
  command: ['sh', '-c', 'do echo World; sleep 2; done;']
```
    
___
⬅️ [[Multi-Container Pods]] | [[Liveness, Readiness, and Startup Probes]] ➡️
### References
1. https://kubernetes.io/docs/concepts/workloads/pods/init-containers/