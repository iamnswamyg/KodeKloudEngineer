A new java-based application is ready to be deployed on a Kubernetes cluster. The development team had a meeting with the DevOps team to share the requirements and application scope. The team is ready to setup an application stack for it under their existing cluster. Below you can find the details for this:
1.Create a namespace named tomcat-namespace-nautilus.
2.Create a deployment for tomcat app which should be named as tomcat-deployment-nautilus under the same namespace you created. Replica count should be 1, the container should be named as tomcat-container-nautilus, its image should be gcr.io/kodekloud/centos-ssh-enabled:tomcat and its container port should be 8080.
3.Create a service for tomcat app which should be named as tomcat-service-nautilus under the same namespace you created. Service type should be NodePort and nodePort should be 32227.
Before clicking on Check button please make sure the application is up and running.
You can use any labels as per your choice.
Note: The kubectl on jump_host has been configured to work with the kubernetes cluster.

```
kubectl get namespace
kubectl get pods
kubectl create namespace tomcat-namespace-nautilus
kubectl get namespace
vi /tmp/tomcat.yaml
[
apiVersion: v1
kind: Service
metadata:
  name: tomcat-service-nautilus
  namespace: tomcat-namespace-nautilus
spec:
  type: NodePort
  selector:
    app: tomcat
  ports:
    - port: 80
      protocol: TCP
      targetPort: 8080
      nodePort: 32227
---
apiVersion: apps/v1
kind: Deployment
metadata:
  name: tomcat-deployment-nautilus
  namespace: tomcat-namespace-nautilus
spec:
  replicas: 1
  selector:
    matchLabels:
      app: tomcat
  template:
    metadata:
      labels:
        app: tomcat
    spec:
      containers:
        - name: tomcat-container-nautilus
          image: gcr.io/kodekloud/centos-ssh-enabled:tomcat
          ports:
            - containerPort: 8080

]
kubectl create -f /tmp/tomcat.yaml
kubectl get deploy -n tomcat-namespace-nautilus
kubectl get pods -n tomcat-namespace-nautilus
kubectl exec tomcat-deployment-nautilus-7fcd865f5d-w7w9v -n tomcat-namespace-nautilus -- curl http://localhost:8080
```