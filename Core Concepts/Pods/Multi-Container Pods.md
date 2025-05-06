___
- Sometimes, two services need to work together, like:
    - A web server
    - A logging agent
- You want them work as a pair and be independent of each other    
- For these kinds of tasks, Multi-container pods are created and they can share same networks as well as same volumes
- There are three common patterns for using multiple containers in a pod:
    - **Sidecar**
    - **Adapter**
    - **Ambassador**
___
   
## How to create 

- In the pod YAML, under `spec`, the `containers` field is an array.
- This allows you to define multiple containers in a single pod
```yaml
    spec:
      containers:
        - name: web-server
          image: web-server-image
        - name: logger
          image: logger-image
```
- One container runs a `web server`
- Another container named `logger` handles logging    
___

## Patterns

1. Sidecar Pattern
- A helper container runs alongside the main one which we saw above.
- Example: a logger that collects logs from the web server
    
2. Adapter Pattern
- It is used to transform or modify data before it’s sent out.
- Example: adapter container converts logs to a common format before sending to the logger
        
3. Ambassador Pattern
-  Works like a proxy for network requests.  
- Example: Your app connects to different databases so instead of changing the app code, the ambassador container reroutes requests to the right database 
          
___

## Note:
- Regardless of which pattern you choose, the definition remains the same.
___

⬅️ [[Node Affinity]] | [[Init Containers]] ➡️
