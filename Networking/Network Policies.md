___
- Network Policies allows you to control how [[Pod]] communicate with each other and with other network entities
___
## Definitions:
- Ingress traffic: Traffic coming into a pod
- Egress traffic: Traffic leaving a pod

___
## Why Network Policies?
- By default, Kubernetes allows all traffic between pods, but by defining network policies can let you restrict this communication.
- Let’s say the team wants to ensure:
	- The frontend cannot access the database directly.
	- Only the API server should be able to talk to the DB on port 3306.
- This is where Network Policies comes into play. They allow you to:
	- Define rules about who can send traffic to a pod (Ingress).    
	- Define rules about where a pod can send traffic (Egress).
___
## How Network Policies Work

- Network Policies are defined using:
	- `podSelector`: Which pods the policy applies to
	- `policyTypes`: Either `Ingress`, `Egress`, or both
	- `rules`: Specific rules that allow traffic based on pod labels and ports
- Important:
	- Policies deny all traffic by default unless it is explicitly allowed.
___
## Example Use Case
To allow only API server to talk to the DB server on port 3306:
1. Label the DB server: `server=db`
2. Label the API server: `server=api`
3. Create a NetworkPolicy like:
    

```yaml
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: db-policy
spec:
  podSelector:
    matchLabels:
      server: db
  policyTypes:
  - Ingress
  ingress:
  - from:
    - podSelector:
        matchLabels:
          server: api
    ports:
    - protocol: TCP
      port: 3306
```

___
## Granular NetworkPolicy

- Above policy would allow any API pod with matching label in any namespace
___
#### Add `namespaceSelector`

```yaml
ingress:
  - from:
	- podSelector:
	    matchLabels:
	      server: api
	- namespaceSelector:
	    matchLabels:
	      team: team-a
```


---

#### Allow External Access

- External sources can't be matched using pod/namespace selectors
- Use `ipBlock` to allow access from an IP address 

```yaml
from:
- ipBlock:
    cidr: 192.168.5.10/32
```

___
#### Common Mistake: Dashes Create New Rules
- These are two (OR condition):
```yaml
from:
- podSelector: {...}
- namespaceSelector: {...}
```

- But below means both must be satisfied (AND condition):

```yaml
from:
- podSelector: {...}
  namespaceSelector: {...}
```

___
⬅️ [[]] | [[Ingress]] ➡️
### References
1. https://kubernetes.io/docs/concepts/services-networking/network-policies/