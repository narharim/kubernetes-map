___
|**Condition**|**Description**|
|---|---|
|`PodScheduled`|The pod has been successfully scheduled onto a node.|
|`Initialized`|All init containers have completed successfully.|
|`ContainersReady`|All containers in the pod are running and ready.|
|`Ready`|The pod is ready to accept and serve requests.|
___
⬅️ [[Pod Lifecycle]] | [[Readiness Probes]] ➡️
### References
1. https://github.com/kubernetes/kubernetes/blob/v1.32.0/pkg/apis/core/types.go