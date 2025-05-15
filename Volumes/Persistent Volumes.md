___
## Problem with Volumes
- When working in large setup, using [[Volumes]] directly defined inside the pod spec can be challenging to manage
- If the underlying storage changed, all pod definitions needed updates.
___
## Solution
-  Persistent Volumes allows us to centralise and decouple storage configuration from pod specs.

___
## What is it
- It is a cluster-wide resource that provides abstracted, reusable storage for users.

___
## Configured with:
####  Access Modes: 
- How the volume can be accessed
	-   'ReadWriteOnce' - one node can mount read/write
	-  'ReadOnlyMany' - many nodes can mount read-only
	- 'ReadWriteMany' - many nodes can mount read/write
#### Capacity: 
- how much storage is available
#### Storage backend:
- can be local (`hostPath`) or remote (e.g., NFS, AWS EBS, etc.)

___
## Example:

```yaml
apiVersion: v1
kind: PersistentVolume
metadata:
  name: pv-vol1
spec:
  capacity:
    storage: 1Gi
  accessModes:
    - ReadWriteOnce
  hostPath:
    path: /data
```
___
## Commands
1. create persistent volumes
>`kubectl create -f pv-definition.yml` 
2. get persistent volumes
> `kubectl get pv`
___
⬅️ [[Volumes]] | [[Persistent Volumes Claims]] ➡️
### References
1. https://kubernetes.io/docs/concepts/storage/persistent-volumes/