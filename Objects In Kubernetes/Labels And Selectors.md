-  Labels are like tags which you attach to [[K8s Objects]] and helps in identifying their properties (e.g., env: prod, tier: backend) 
- Selectors are used to select/filter items based on these labels.  
- Example:
    - Add labels like `env=prod` 
    - Then run: `kubectl get pods --selector env=prod` to view only those pods which has `env` value prod`.
- Over time, your cluster may have thousands of objects so labels help group and filter them.
    
___
## How to Add Labels
- Add them in the pod definition file under `metadata.labels`:
    ```yaml
    metadata:
      labels:
        env: prod
    ```
    
___
## Connecting Objects
- Kubernetes uses labels and selectors internally to connect objects.

#### ReplicaSet Example:
- In a [[ReplicaSets]] YAML, there are **two label sections**:
	 1. Top-level labels → for ReplicaSet object itself
     2. Inside `template.metadata.labels` → for the pods it manages  
- If matches, the labels defined on Pods to decide which ones it should manage

#### Services Example:
- [[Service]] also uses selectors to find which Pods to connect to.
- It matches the labels defined on Pods to decide which ones it should send traffic to.

#### Multiple Labels:
- If multiple pods share same label (e.g., `app=yoda`), but do different things,you can use extra labels to make the selector more specific.

___
⬅️ [[Cron Job]] | [[Blue Green and Canary Deployment]] ➡️
### References
1. https://kubernetes.io/docs/concepts/overview/working-with-objects/labels/

