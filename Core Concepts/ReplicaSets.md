___
- The ReplicaSet ensures that the specified number of pods is always running.
- For example: If we specify the number of pods as 3 for a ReplicaSet, then at any given point, the number of pods running will be 3.    
- If there are more than 3 pods, the ReplicaSet will terminate the extra pods, and if there are fewer than 3 pods, the ReplicaSet will start new pods.
- In short, the pods are now maintained by the ReplicaSet. It will automatically replace pods that are unhealthy.
___
```yaml
apiVersion: apps/v1
kind: ReplicaSet
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

___

- The `.spec` is the section where you define the desired state for the ReplicaSet object. It consist of  `replicas`, `selector`, and `template` (pod template). This all are mandatory fields
- The `.spec.replicas` is a field that specifies the desired number of pod you want to run at any given time.
- The `.spec.selector` is a label selector which tells the ReplicaSet how to find which Pods it should manage.
- The `.spec.template` is a pod template that ReplicaSet will manage.
- The `.spec.template.metadata.labels` are the labels given to the pod which will be manage/created by this ReplicaSet. This is crucial as ReplicaSet will manages all the pods with labels that match the selector and hence `.spec.template.metadata.labels` must be equal to the `.spec.selector`.  See [[Labels And Selectors]]
___

⬅️ [[Pod]] | [[Deployment]] ➡️
### References
1. https://kubernetes.io/docs/concepts/workloads/controllers/replicaset/