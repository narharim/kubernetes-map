___
## Imagine This

- You have a room freshly painted with a strong smell.
- People find the smell unbearable, so they avoid entering.
- Painters used mask so they can tolerate it and still go in.
___
- In Kubernetes:
	- The room is a node 
	- The people is pods (applications to be placed)  
	- The smell is a taint (set on the node)
	- The tolerance to the smell is a toleration (set on the pod)
___
## Idea
- In short you can control what pods go on which nodes with a limitation (discussed below)
- Taints are like saying: "This room smells! Don't come in unless you can handle it."
- Tolerations are like people saying: "I’m okay with the smell, I can enter."
    
___
## Taint Effects

1. NoSchedule : Don't allow anyone unless they tolerate the smell.
2. PreferNoSchedule: Try not to allow anyone, but okay if there's no choice.
3. NoExecute: Kick out people already inside and don’t allow new ones unless they can handle it. (sorry for this example dont kick say politely..hahaha)
    
___

## Toleration
- To add toleration to a pod:  
     
    ```yaml
    tolerations:
    - key: "room"
      operator: "Equal"
      value: "strong-smell"
      effect: "NoSchedule"
    ```
___
## Flow:
- Default Behavior:  
    - If no taints exist, scheduler schedules the pods across nodes evenly
- Add a taint `room=strong-smell:NoSchedule` to node one
- Adding a Toleration to a Pod B
- Now only Pod B can enter node one others get blocked
___
## Master Nodes

- Master nodes by default has a taint. So no pod gets placed there.
- Best practice: don’t place workloads on the master node.
___
## Keep in Mind
- Taints do not guarantee placement. They just block pods without tolerations.
- If no restriction is on other nodes, a tolerating pod can go there too.

___

## Commands 
1. To taint a node:
> `kubectl taint nodes node1 room=strong-smell:NoSchedule`
___

⬅️ [[Service Accounts]] | [[Node Affinity]] ➡️
### References
1. https://kubernetes.io/docs/concepts/scheduling-eviction/taint-and-toleration/