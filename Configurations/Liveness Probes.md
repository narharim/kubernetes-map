___
- By default, when application inside container crashes,  Kubernetes will try to restart the [[Pod]] in order to serve requests.
- In real-world scenarios, when application is not working due to bug and container continues to stay alive. In that scenario they are unable to serve requests.
- We need a way to check periodically that the application inside the container is healthy or not
- Kubernetes provides several ways to check that the application are healthy
    - Set up an HTTP endpoint (for web servers)
    - Use a TCP socket check (e.g., for databases)        
    - Write and execute a custom script inside the container to verify liveness

___
## How to Define a Liveness Probe
- In the Pod YAML definition, under the `spec.containers` section, define a `livenessProbe`:
#### HTTP Endpoint Example
```yaml
containers:
  - name: web-server
    image: web-server-image
    livenessProbe:
      httpGet:
        path: /api/healthy
        port: 8080
```

#### TCP Socket Example
```yaml
livenessProbe:
  tcpSocket:
    port: 3306
```

#### Custom Script Example
```yaml
livenessProbe:
  exec:
    command:
      - python3
      - check_health.py
```
___
#### Additional Fields
- `initialDelaySeconds`: If your application takes some time to warm up (e.g., 10 seconds), use this field to specify the delay before the first probe is initiated.
- `periodSeconds`: Specifies how often the probe should be performed.
- `failureThreshold`: By default, Kubernetes tries 3 times checking container is not ready. You can increase this threshold (e.g., to 10) to allow more retries before failing.
___
⬅️ [[Readiness Probes]] | [[Startup Probes]] ➡️

### References

1. https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-startup-probes/
    