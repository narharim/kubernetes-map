- Allows us to set limit to resources available in namespace


### CPU Resource constraint
```yaml
apiVersion: v1
kind: LimitRange
metadata:
  name: cpu-resource-constraint
spec:
  limits:
  - default: # this section defines default limits
      cpu: 500m
    defaultRequest: # this section defines default requests
      cpu: 500m
    max: # max and min define the limit range
      cpu: "1"
    min:
      cpu: 100m
    type: Container

```

### Memory Resource constraint
```yaml
apiVersion: v1
kind: LimitRange
metadata:
  name: memory-resource-constraint
spec:
  limits:
  - default: # this section defines default limits
      memory: 1Gi
    defaultRequest: # this section defines default requests
      memory: 1Gi
    max: # max and min define the limit range
      memory: 1Gi
    min:
      memory: 500m
    type: Container

```
---
⬅️ [[Resource Requirement]] | [[Service Accounts]] ➡️
### References
1. https://kubernetes.io/docs/concepts/policy/limit-range/