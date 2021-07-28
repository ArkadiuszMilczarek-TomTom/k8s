Enable minikube ingress controller
```bash
minikube addons enable ingress
```
---
create mogno db:
```bash
kubectl apply -f 0_mongodb.yaml
 ```

init cluster:
```bash
kubectl exec mongodb-statefulset-0 -c mongodb -- mongo --eval 'rs.initiate({_id: "MainRepSet", version: 1, members: [ {_id: 0, host: "mongodb-statefulset-0.mongodb-service.default.svc.cluster.local:27017"}, {_id: 1, host: "mongodb-statefulset-1.mongodb-service.default.svc.cluster.local:27017"}, {_id: 2, host: "mongodb-statefulset-2.mongodb-service.default.svc.cluster.local:27017"} ]});'
```
```bash
kubectl exec mongodb-statefulset-0 -c mongodb -- mongo --eval 'rs.status();'
```
```bash
kubectl exec mongodb-statefulset-0 -c mongodb -- mongo --eval 'db.getSiblingDB("admin").createUser({user:"myTestUser",pwd:"mySecretPassword",roles:[{role:"root",db:"admin"}]});'
```

---
create config
```bash
kubectl apply -f 1_config.yaml
```

---
create mongo-express with service
```bash
kubectl apply -f 2_mongo_express.yaml
```

enable minikube service:
```bash
minikube service mongo-express-service
```

---
user ingress
- change `mongo-express-service` to internalIp
- create ingress:
```bash
 kubectl apply -f 4_ingress.yaml
```

get ingress ip
```bash
kubectl get ingress
```
edit etc/hosts, add:  `<ingress_ip>     mongofront.local`  

check data consistency
```bash
mongo
#rs.slaveOk() # if executed on slave
db.adminCommand( { listDatabases: 1 } )
use mydb
db.getCollectionNames()
db.user.find()
```

---
# HELM ->
