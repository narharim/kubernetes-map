
---
- Secrets are used to pass sensitive data in the form of key-value pairs.
- Secrets are similar to [[ConfigMaps]] but are specifically intended to hold confidential data.
- Secrerts are not encrypted only base64 encoded. user must enable encryption at rest

```yaml
apiVersion: v1
kind: Secret
metadata:
  name: my-secret
data:
  key1: c2VjcmV0MQ==
  key2: c2VjcmV0Mg==

```

To get secrets. we can define it in pod definition file
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
	      - secretRef:
		      name: my-secret
```
To get single env from secret we can use
```yaml
        env:
	      - name: key1
	        valueFrom:
			    secretKeyRef:
			      name: my-secret
			      key: key1
```
## Commands
1. create secret without YAML (imperative command)
>`kubectl create secret generic <name>`
2. create secret with YAML (declarative command)
> `kubectl create -f secret-definition.yaml`
3. create secret with values 
> `kubectl create secret generic my-secret --from-literal=key1=secret1 --from-literal=key2=secret2`
4. create secret from file
> `kubectl create secret my-secret --from-file=path/to/file`
5. get secret
>`kubectl get secret`
6. describe secret
> `kubectl describe configmaps`

⬅️ [[ConfigMaps]] | [[Security Context]] ➡️
### References
1. https://kubernetes.io/docs/concepts/configuration/secret/