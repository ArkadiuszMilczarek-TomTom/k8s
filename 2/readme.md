Start nginx
```
kubectl create deployment nginx-deployment --image=nginx
```
---
List resources:
```
kubectl get deployment
kubectl get replicaset
kubectl get pod
kubectl get deployment,replicaset,pod
```

```
kubectl get deploy/nginx-deployment -o yaml
```

--- 
Edit nginx:
- set image version
- set 3 replicas
```
kubectl edit deployment nginx-deployment
```

---
debug pods:
```
kubectl logs <POD_NAME>
kubectl exec -it <POD_NAME> -- bin/bash
```

--- 
Delete
```
kubectl delete pod <POD_NAME>
```
```
kubectl delete deployment nginx-deployment
```