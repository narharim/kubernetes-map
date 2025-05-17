___
- A Persistent Volume Claim is a request for storage by a user or an application.
- Users don't deal with how the storage is provisioned they just ask for how much they need
- Kubernetes tries to match the claim with a suitable [[Persistent Volumes]].
- Once matched, the PV and PVC are bound one-to-one

___
### How Binding Works
- First it finds a PV that has equal or more capacity than requested.      
- If it matches Access Modes ([[Persistent Volumes#Access Modes]]), and [[StorageClass]] it is automatically binded
- But if multiple volumes are suitable, you can use [[Labels And Selectors]] to target a specific PV.
- If no suitable volume is available then PVC remains in `Pending` state and once a matching PV is added, it binds automatically.
___
## PVC Example Manifest

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
      storage: 500Mi
```
___
## One-to-One Binding

- A PVC is bound to only one PV. Even if the PV has more capacity than requested, it can’t be split across multiple claims.

For example:
- Claim requests 500Mi
- PV has 1Gi
- PVC is binded to that PV  
- The remaining 500Mi is unused and unavailable to other claims
    
___
## When a PVC is Deleted?

The  `persistentVolumeReclaimPolicy` of the PV determines the behavior:

### 1. `Retain` (default)
- PV remains even if the PVC is deleted.
- Admin must manually delete or reuse the volume.

### 2. `Delete`
- Underlying storage is automatically deleted when the PVC is deleted.

### 3. `Recycle` (deprecated)
- PV is scrubbed and reused for future claims.
---

## Commands
- Create PVC
>`kubectl create -f pvc.yaml`
- Get PVC
> `kubectl get pvc`
___
⬅️ [[Persistent Volumes]] | [[StorageClass]] ➡️
### References
1. 