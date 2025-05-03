- Node affinity is a way to control where a pod should be placed, by attracting it to certain nodes based on labels.

___
## Node Affinity Configuration

In your pod definition, under `spec`, you define:

```yaml
affinity:
  nodeAffinity:
    requiredDuringSchedulingIgnoredDuringExecution:
      nodeSelectorTerms:
        - matchExpressions:
            - key: size
              operator: In
              values:
                - large
```

- `key`: The label key on the node (e.g., `size`)
- `operator`: `In`, `NotIn`, or `Exists`
- `values`: What the pod is looking for (e.g., `large`, `medium`)

___
## Types of Node Affinity

1. **RequiredDuringSchedulingIgnoredDuringExecution**
- During scheduling: Pod _must_ land on a matching node.
- During execution: Pod _continues running_ even if node labels change.
    
2. **PreferredDuringSchedulingIgnoredDuringExecution**
- During scheduling: Pod _tries_ to go to a matching node, but will schedule elsewhere in certain scenario.
- During execution: Pod _continues running_ even if node labels change.
        
___

## Node Affinity vs. Taints and Tolerations

- Node Affinity: Pulls pods _toward_ nodes 
- Taints and Tolerations: Pushes pods _away_ from nodes 

___
⬅️ [[Taints and Tolerations]] | [[Multi-Container Pods]] ➡️
### References
1.