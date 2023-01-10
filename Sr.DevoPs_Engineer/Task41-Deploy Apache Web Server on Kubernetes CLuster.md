There is an application that needs to be deployed on Kubernetes cluster under Apache web server. The Nautilus application development team has asked the DevOps team to deploy it. We need to develop a template as per requirements mentioned below:
1. Create a namespace named as httpd-namespace-xfusion.
2. Create a deployment named as httpd-deployment-xfusion under newly created namespace. For the deployment use httpd image with latest tag only and remember to mention the tag i.e httpd:latest, and make sure replica counts are 2.
3. Create a service named as httpd-service-xfusion under same namespace to expose the deployment, nodePort should be 30004.
Note: The kubectl utility on jump_host has been configured to work with the kubernetes cluster.

```
kubectl create namespace httpd-namespace-xfusion
vi /tmp/httpd.yaml
[
apiVersion: v1
kind: Service
metadata:
  name: httpd-service-xfusion
  namespace: httpd-namespace-xfusion
spec:
  type: NodePort
  selector:
    app: httpd_app_xfusion
  ports:
    - port: 80
      targetPort: 80
      nodePort: 30004
---
apiVersion: apps/v1
kind: Deployment
metadata:
  name: httpd-deployment-xfusion
  namespace: httpd-namespace-xfusion
  labels:
    app: httpd_app_xfusion
spec:
  replicas: 2
  selector:
    matchLabels:
      app: httpd_app_xfusion
  template:
    metadata:
      labels:
        app: httpd_app_xfusion
    spec:
      containers:
        - name: httpd-container-xfusion
          image: httpd:latest
          ports:
            - containerPort: 80

]
kubectl create -f /tmp/httpd.yaml
kubectl get pods -n httpd-namespace-xfusion
```