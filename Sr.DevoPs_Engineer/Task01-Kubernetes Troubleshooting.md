One of the Nautilus DevOps team members was working on to update an existing Kubernetes template. Somehow, he made some mistakes in the template and it is failing while applying. We need to fix this as soon as possible, so take a look into it and make sure you are able to apply it without any issues. Also, do not remove any component from the template like pods/deployments/volumes etc.
/home/thor/mysql_deployment.yml is the template that needs to be fixed.
Note: The kubectl utility on jump_host has been configured to work with the kubernetes cluster.

```
cd /home/thor/
vi mysql_deployment.yml
mkdir /task
cp mysql_deployment.yml /task/mysql_deploy.yml
cp mysql_deployment.yml /task/mysql_svc.yml
cp mysql_deployment.yml /task/mysql_pvc.yml
cp mysql_deployment.yml /task/mysql_pv.yml
cd /task
vi mysql_pv.yml
[
apiVersion: v1
kind: PersistentVolume
metadata:
  name: mysql-pv
  labels:
    type: local
spec:
  storageClassName: standard
  capacity:
    storage: 250Mi
  accessModes:
    - ReadWriteOnce
  hostPath:
    path: "/mnt/data"
  persistentVolumeReclaimPolicy: Retain

]
kubectl create -f mysql_pv.yml
kubectl get pv
vi mysql_pvc.yml
[
---
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: mysql-pv-claim
  labels:
    app: mysql-app
spec:
  storageClassName: standard
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 250Mi    
]
kubectl create -f mysql_pvc.yml
kubectl get pvc
vi mysql_svc.yml
[
---
apiVersion: v1
kind: Service
metadata:
  name: mysql
  labels:
    app: mysql-app
spec:
  type: NodePort
  ports:
    - targetPort: 3306
      port: 3306
      nodePort: 30011
  selector:
    app: mysql-app
    tier: mysql    
]
kubectl create -f mysql_svc.yml
kubectl get svc
vi mysql_deploy.yml
[
---
apiVersion: apps/v1
kind: Deployment
metadata:
  name: mysql-deployment
  labels:
    app: mysql-app
spec:
  selector:
    matchLabels:
      app: mysql-app
      tier: mysql
  strategy:
    type: Recreate
  template:
    metadata:
      labels:
        app: mysql-app
        tier: mysql
    spec:
      containers:
      - image: mysql:5.6
        name: mysql
        env:
        - name: MYSQL_ROOT_PASSWORD
          valueFrom:
            secretKeyRef:
              name: mysql-root-pass
              key: password
        - name: MYSQL_DATABASE
          valueFrom:
            secretKeyRef:
              name: mysql-db-url
              key: database    
        - name: MYSQL_USER
          valueFrom:
            secretKeyRef:
              name: mysql-user-pass
              key: username
        - name: MYSQL_PASSWORD
          valueFrom:
            secretKeyRef:
              name: mysql-user-pass
              key: password
        ports:
        - containerPort: 3306
          name: mysql
        volumeMounts:
        - name: mysql-persistent-storage
          mountPath: /var/lib/mysql
      volumes:
      - name: mysql-persistent-storage
        persistentVolumeClaim:
          claimName: mysql-pv-claim
]
kubectl create -f mysql_deploy.yml
kubectl get deploy //check if all working
//then delete everything
kubectl delete deploy mysql-deployment
kubectl delete svc mysql
kubectl delete pvc mysql-pvc-claim
kubectl delete pv mysql-pv
//recheck everything
kubectl get deploy
kubectl get svc
kubectl get pvc
kubectl get pv
//delete content in mysql_deployment.yml
cat mysql_pv.yml mysql_pvc.yml mysql_svc.yml mysql_deploy.yml /home/thor/mysql_deployment.yml
kubectl create -f /home/thor/mysql_deployment.yml
```