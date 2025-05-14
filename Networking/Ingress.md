___
## Problem

- When you deploy multiple applications, exposing them to the internet in a cost-efficient as well as in secure way becomes tricky. Without Ingress, you either have to:
1. Use multiple LoadBalancer services which will increase costs.
2. Use NodePort services + external proxy which leads to a complex configuration.
3. Deal with DNS, SSL, routing logic separately which is harder to manage.

___
## Ingress to Rescue
 - Its API object that manages external access to services within a cluster.
 - It allows you to define rules for routing traffic based on hostnames or URL paths.


___
## Core Components of Ingress

1. Ingress Resource : These are rules that specify how to route external traffic to internal services.
2. Ingress Controller: A component that implements the Ingress rules. Kubernetes as a project supports and maintains AWS, GCE and nginx ingress controllers.


```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: ingress-example
  annotations:
    nginx.ingress.kubernetes.io/rewrite-target: /
spec:
  rules:
  - host: myapp.com
    http:
      paths:
      - path: /api
        pathType: Prefix
        backend:
          service:
            name: api-service
            port:
              number: 80
      - path: /web
        pathType: Prefix
        backend:
          service:
            name: web-service
            port:
              number: 80

```


___
⬅️ [[]] | [[]] ➡️
### References
1.
