
---
- ConfigMaps are used to pass configuration data in the form of key-value pairs.
- Pod can consume these key-value pairs as environment variables for the application running inside it.
```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: my-config
data:
  key1: config1
  key2: config2

```

To get config maps key-value pairs as environment variables. we can define it in pod definition file
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: server
  labels:
    env: sandbox
spec:
   containers:
      - name: nginx
        image: nginx
        envFrom: 
	      - configMapRef:
		      name: my-config
```
To get single env from config we can use
```yaml
        env:
	      - name: key1
	        valueFrom:
			    configMapKeyRef:
			      name: my-config
			      key: key1
```
## Commands
1. create configmap without YAML (imperative command)
>`kubectl create configmap <name>`
2. create configmap with YAML (declarative command)
> `kubectl create -f configmap-definition.yaml`
3. create configmap with values 
> `kubectl create configmap my-config --from-literal=key1=config1 --from-literal=key2=config2`
4. create configmap from file
> `kubectl create configmap my-config --from-file=path/to/file`
5. get configmaps
>`kubectl get configmaps`
6. describe configmaps
> `kubectl describe configmaps`

⬅️ [[Service]] | [[Secrets]] ➡️
### References
1. https://kubernetes.io/docs/concepts/configuration/configmap/