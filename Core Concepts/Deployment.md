___
- Deployment is like a manager in kubernetes.
- Deployment manages ReplicaSets, supports rollbacks, and updates the currently running application version.
- Definition for creating Deployment is same as ReplicaSets. Value of `kind` field is replaced with `Deployment`
___
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: server
  labels:
    app: webserver
    env: prod
spec:
  replicas: 3
  selector:
    matchLabels:
      env: prod
  template:
    metadata:
      labels:
        env: prod
    spec:
      containers:
      - name: nginx
        image: nginx

```
---

- The `.spec.replicas` is a field that specifies the desired number of pod you want to run at any given time.
- The `.spec.selector` is a label selector which tells the ReplicaSet how to find which Pods it should manage.
- The `.spec.template` is a pod template that ReplicaSet will manage.
- The `.spec.template.metadata.labels` are the labels given to the pod which will be manage/created by ReplicaSet. This is crucial as ReplicaSet will manages all the pods with labels that match the selector and hence `.spec.template.metadata.labels` must be equal to the `.spec.selector`. 
---
## Rollout and Versioning
- when we create `Deployment` it creates a rollout of new version of applications and new revision of `Deployment` is created.
- If the current revision has some errors we can revert back to older `Deployment` 

## Deloyment Strategy
- `Recreate` and `RollingUpdate` strategy are used to deploy new version of application
- `Recreate` will bring all pods down and starts new ones with new version
- `RollingUpdate` will bring one pod down and start new one and so on
- `RollingUpdate` is default strategy
___
## Commands
1. create deployment
>`kubectl create -f deployment-definition.yml` 

2. get deplotment
> `kubectl get deployments`
3. describe deployment
>`kubectl describe deployment <deployment-name>`
4. rollout status
>`kubectl rollout status <deployment-name>`
5. rollout history
>`kubectl rollout history <deployment-name>`
6. rollout undo
>`kubectl rollout undo <deployment-name>`

___
⬅️ [[ReplicaSets]] | [[Service]] ➡️
### References
1.