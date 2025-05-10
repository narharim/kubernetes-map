___
-  These aren’t built-in like `RollingUpdate` or  `Recreate` that we saw in [[Deployment]] but  can be implemented using Deployments and Services.
___
## Blue Green Deployment
- Run two versions of your app:    
    - Blue = old version (e.g., `v1`)
    - Green = new version (e.g., `v2`)    
- 100% traffic goes to blue at first
- You will take below steps:
    1. Deploy green version (new deployment)
    2. Run tests on green version
    3. Once satisfied, switch traffic from blue to green
        
## How to switch

- Pods have labels like `version: v1` or `version: v2`
- Service routes traffic using label selectors
    - Initially: `selector: version=v1`    
    - After testing: change to `selector: version=v2`
- Now the service routes all traffic to the green (new) deployment

___
## Canary Deployment

- Canary deployment allows you deploy a new version of the app is deployed alongside the existing version.
- Only a small portion of the traffic is routed to the new version while the majority stays to on the stable version
- This allows testing the new version with real traffic before fully rolling it out.

___
## Limitation
- Traffic splitting is based on the number of pods.
- Precise traffic control is not possible with basic Deployments and Services.

___
⬅️ [[Labels And Selectors]] | [[Jobs]] ➡️
