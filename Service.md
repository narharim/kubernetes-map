# Service
---
- Service helps connect applications inside the cluster or to external users. 
- Pods can die and new ones may be created with different IP addresses.
- Service provides a stable IP address and DNS name to access a group of Pods.
- It's like a permanent door to access underlying pods
```yaml
apiVersion: v1
kind: Service
metadata:
  name: my-service
spec:
  type: NodePort
  selector:
    app: myapp
  ports:
    - port: 80
      targetPort: 80
      nodePort: 30007
```

- `selector` should have pods labels which needs to be exposed
- By default `targetPort` is set to  the same value as the `port` field
- By default, Kubernetes control plane will allocate a `nodePort` from a range (default: 30000-32767) (optional)
  
## Service Types
- Service types allow you to specify what kind of Service you want.
    
### NodePort
- Service listens on a port on each Node and forwards the request to the Pod where our application is running.
    
### ClusterIP
- Service creates a virtual IP inside the cluster to connect with other applications.
    
### LoadBalancer
- Service provisions a LoadBalancer to expose our application externally in a cloud environment.


## Commands

1. create a service
> `kubectl create -f service-definition.yml`

2. get all services
> `kubectl get svc`

3. describe service
> `kubectl describe svc <service-name>`

4. expose a pods as a service
> `kubectl expose pod <pod-name> --port=80 --name <service-name> --type=NodePort`

⬅️ [[Deployment]] | [[ConfigMap]] ➡️
### References
1. https://kubernetes.io/docs/concepts/services-networking/service/