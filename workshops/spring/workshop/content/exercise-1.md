```editor:append-lines-to-file
file: ~/exercises/deploy/ingress.yaml
text: |
  apiVersion: networking.k8s.io/v1
  kind: Ingress
  metadata:
    name: tanzu-app
    labels:
        app: tanzu-app
  spec:
    rules:
    - host: {{session_namespace}}-app.{{ingress_domain}}
      http:
        paths:
        - path: "/"
          pathType: Prefix
          backend:
            service:
              name: react-ui
              port:
                number: 80
        - path: "/api"
          pathType: Prefix
          backend:
            service:
              name: spring-api-1
              port:
                number: 8080
```

```terminal:execute
command: kubectl apply -f deploy/.
clear: true
```
