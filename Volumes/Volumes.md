___
## In Docker
- when a container is destroyed its data is lost
- docker uses volumes to persist data which are directories on the host mounted into the container. (Bind Mount)
___
## In Kubernetes
- Similarly, when a [[Pod]] is destroyed its data is lost
- [[Volumes]] allow data to persist beyond the life of a pod.
___
## How Volumes Works

- Attach a volume to a pod and mount it into the container.
- Example: 
	  - Attach  `/data` on Pod using `hostPath` field.
	  - Mount the volume to '/opt' in the container.

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: my-first-volume
spec:
  containers:
  - name: example-container
    image: registry.k8s.io/test-webserver
    volumeMounts:
    - mountPath: /opt
      name: example-volume
  volumes:
  - name: example-volume
    hostPath:
      path: /data # directory location on host
```
___
##  Limitations of `hostPath`

- Works only in single-node clusters.
- In a multi-node cluster, using `hostPath` leads to inconsistency:
	- Each node has its own separate `/data` dir.
___
⬅️ [[]] | [[Persistent Volumes]] ➡️
### References
1. https://kubernetes.io/docs/concepts/storage/volumes/
