___
- There are two types of accounts in Kubernetes:
    1. User accounts → used by humans (admins, developers).
    2. Service accounts → used by applications/machines.

- When an application talks to the Kubernetes API, it needs to be authenticated. This is done by using a service account.
    
___

### Default Service Account
- Kubernetes automatically creates a token (used for authentication) and stores it as a secret object. (Deprecated)    
- Every namespace has a default service account.    
- If you don’t specify a service account in the pod spec, the default one is used.
- To avoid automatic token mount in spec section, use below field:
    
    ```yaml
    automountServiceAccountToken: false
    ```

- Kubernetes mounts the token (default serviceaccount) into the pod
- The token is in `/var/run/secrets/kubernetes.io/serviceaccount`
___
## Limitations of Default Account
- It has **very limited permissions**.
    
- To use a custom service account specify it in the pod spec 
	```yaml
	serviceAccountName: <name>
	``` 

___
## Changes in Kubernetes 1.22

- Older tokens:
    - Had no expiry and and were not audience-bound and were stored in a secret per service account.    
    - Posed security and scalability issues.
- Kubernetes added a TokenRequest API:
    - Generates time-bound, audience-bound, object-bound tokens
    - Token is created on-the-fly and mounted as a projected volume, not stored in a secret.
___        
## Changes in Kubernetes 1.24

- Service accounts no longer create secrets automatically.

___
## What if you want Old Behaviour?
- You can manually create a secret like this:
    
    ```yaml
    kind: Secret
    type: kubernetes.io/service-account-token
    metadata:
      annotations:
        kubernetes.io/service-account.name: <name>
    ```
    
- But it’s not recommended unless absolutely necessary as these tokens are non-expiring, which poses a security risk.
___
## Best Practice

- Use TokenRequest API  
- Avoid creating non-expiring token secrets
___
## Commands
1. Create a service account 
>`kubectl create sa <name>`
2. view a service account  
> `kubectl get sa`
3. view token
> `kubectl describe secret <name>`
4. To create a token:
> `kubectl create token <service-account-name>`
___

⬅️ [[Limit Range]] | [[Taints and Tolerations]] ➡️
### References
1. https://kubernetes.io/docs/concepts/security/service-accounts/
2. https://kubernetes.io/docs/concepts/configuration/secret/#serviceaccount-token-secrets
3. https://github.com/kubernetes/enhancements/issues/2799
4. https://github.com/kubernetes/enhancements/blob/master/keps/sig-auth/1205-bound-service-account-tokens/README.md