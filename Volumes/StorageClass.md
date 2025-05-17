___
## Problem
- you have to manually create a disk, then manually create PV ([[Persistent Volumes]]) using that disk, and finally create a PVC ([[Persistent Volume Claims]]) to bind to it. This is called **Static Provisioning**
___
## Dynamic Provisioning 
With Storage Classes, we can automatically provision storage volumes on demand.
#### How it works:
- You define a StorageClass with a provisioner (like GCP, AWS, Azure).
- when a PVC references a StorageClass and Kubernetes automatically calls the provisioner to create a new disk, creates a matching PV, and binds it to the PVC.
___
### StorageClass Example

```yaml
apiVersion: storage.k8s.io/v1
kind: StorageClass
metadata:
  name: standard
provisioner: kubernetes.io/gce-pd
parameters:
  type: pd-standard
  replication-type: none

```

- `provisioner`: defines what backend system to use (e.g., 'kubernetes.io/aws-ebs', 'kubernetes.io/gce-pd')
- `parameters`: disk-specific settings like type ('standard', 'ssd') or replication ('none', 'regional-pd')
___
### PVC Using a StorageClass

```yaml
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: myclaim
spec:
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 1Gi
  storageClassName: standard
```

- The `storageClassName` tells which StorageClass to use.
- You don't need to write a PV definition manually anymore.

___
⬅️ [[Persistent Volume Claims]] | [[]] ➡️
### References
1. https://kubernetes.io/docs/concepts/storage/storage-classes/
