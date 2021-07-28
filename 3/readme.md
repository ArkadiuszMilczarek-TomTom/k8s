```
kubectl apply -f nginx-deployment.yaml
kubectl apply -f nginx-service.yaml
```
---
Pod IP's
```
kubectl get pods -o wide
```

pods <---> service
```
kubectl describe service nginx-service
kubectl get endpoints nginx-service -o yaml
```

---

# **NAMESPACE**