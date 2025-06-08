- A configuration file used by entities for authentication, connecting and getting information of your cluster.
- Default location:  `~/.kube/config`
___
### Manual Authentication 

You can query the API server using:

```bash
curl --cert user.crt --key user.key --cacert ca.crt https://<api-server>:6443/api/v1/pods
```

Or with `kubectl`:

```bash
kubectl get pods \
  --server=https://<api-server>:6443 \
  --certificate-authority=ca.crt \
  --client-certificate=user.crt \
  --client-key=user.key
```

___
### Structure of kubeconfig

 - `clusters`
	  -  Contains info about your clusters
	  -  Includes API server address, certificate authority (CA) details
- `contexts`
    - Connects a user to a cluster
    -  Can optionally specify a default namespace
-  `users`
   -  Defines credentials to access clusters
   -  Can include tokens, client cert/key
-  `current-context`
   - Tells `kubectl` which context to use by default

___
### Example Structure

```yaml
apiVersion: v1
clusters:
- cluster:
    certificate-authority: /home/narhari/.minikube/ca.crt
    server: https://192.168.49.2:8443
  name: minikube
contexts:
- context:
    cluster: minikube
    namespace: default
    user: minikube
  name: minikube
current-context: minikube
kind: Config
preferences: {}
users:
- name: minikube
  user:
    client-certificate: /home/narhari/.minikube/profiles/minikube/client.crt
    client-key: /home/narhari/.minikube/profiles/minikube/client.key

```

___
### Managing Multiple Clusters & Users

- Define multiple clusters (dev, prod, etc.)
- Define multiple users (admin, dev-user, prod-user, etc.)
- Create contexts to map a user to a cluster
___
### Commands
1. View the full kubeconfig
> `kubectl config view`
2. Switch to a different context
> `kubectl config use-context <name>`
3. List all contexts
> `kubectl config get-contexts`
4. Show current context
> `kubectl config current-context`
5. Create or modify a context
> `kubectl config set-context`
6. Add a new cluster
> `kubectl config set-cluster`
7. Add a new user
> `kubectl config set-credentials`

___
⬅️ [[Security Primitives]] | [[API Group]] ➡️
### References
1.