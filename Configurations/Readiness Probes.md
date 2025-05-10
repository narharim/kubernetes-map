___
- By default, Kubernetes assumes that when a [[Pod]] reaches the `Ready` stage, it is capable of serving requests.
- In real-world scenarios, the application may take a few milliseconds (or more) to actually become ready due to initial startup delays.
- We need a way to tie the `Ready` condition to the actual state of the application running inside the container.
- Kubernetes provides several ways to define when applications are ready to serve requests:
    - Set up an HTTP endpoint (for web servers)
    - Use a TCP socket check (e.g., for databases)        
    - Write and execute a custom script inside the container to verify readiness
___
## How to Define a Readiness Probe
- In the Pod YAML definition, under the `spec.containers` section, define a `readinessProbe`:
#### HTTP Endpoint Example
```yaml
containers:
  - name: web-server
    image: web-server-image
    readinessProbe:
      httpGet:
        path: /api/ready
        port: 8080
```

#### TCP Socket Example
```yaml
readinessProbe:
  tcpSocket:
    port: 3306
```

#### Custom Script Example
```yaml
readinessProbe:
  exec:
    command:
      - python3
      - check_status.py
```
___
#### Additional Fields
- `initialDelaySeconds`: If your application takes some time to warm up, use this field to specify the delay before the first probe is initiated.
- `periodSeconds`: Specifies how often the probe should be performed.
- `failureThreshold`: By default, Kubernetes tries 3 times checking container is not ready. You can increase this threshold to allow more retries before failing.
___
⬅️ [[Pod Conditions]] | [[Liveness Probes]] ➡️

### References

1. https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-startup-probes/
    