___
- It helps prevent one team/user from over consuming cluster resources. and give fair usage among multiple teams sharing the same cluster.
- It can enforce limit on compute resources (e.g., `cpu`, `memory`), object counts (e.g., number of Pods, Services)
___
```yaml
apiVersion: v1
kind: ResourceQuota
metadata:
  name: team-a-quota
  namespace: team-a
spec:
  hard:
     cpu: "10"
     memory: "20Gi"
     pods: "10"
```

___
## Commands
1. create resource
> `kubectl create -f quota.yaml`
2. describe quota
> `kubectl describe quota`
___

⬅️ [[]] | [[]] ➡️

### References
1. https://kubernetes.io/docs/concepts/policy/resource-quotas/