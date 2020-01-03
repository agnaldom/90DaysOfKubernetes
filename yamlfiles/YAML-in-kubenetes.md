```
apiVersion: v1
kind: POD
metadata:
  name: myapp-pod
  labels:
       app: myapp
       type: front-end
spec:
  containers:
    - name: nginx-container
      image: niginx
```

Kind        | Version
-----------------------
POD         | v1
Service     | v1
ReplicaSet  | apps/v1
Deployment  | apps/v1

Create pods


```kubectl create -f pod-definition.yml```