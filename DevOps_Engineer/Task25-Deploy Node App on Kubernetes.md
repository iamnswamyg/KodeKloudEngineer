The Nautilus development team has completed development of one of the node applications, which they are planning to deploy on a Kubernetes cluster. They recently had a meeting with the DevOps team to share their requirements. Based on that, the DevOps team has listed out the exact requirements to deploy the app. Find below more details:
1.Create a deployment using gcr.io/kodekloud/centos-ssh-enabled:node image, replica count must be 2.
2.Create a service to expose this app, the service type must be NodePort, targetPort must be 8080 and nodePort should be 30012.
Make sure all the pods are in Running state after the deployment.
You can check the application by clicking on NodeApp button on top bar.
You can use any labels as per your choice.
Note: The kubectl on jump_host has been configured to work with the kubernetes cluster.

```
kubectl get pods
vi /tmp/nodeapp.yaml
[
apiVersion: v1
kind: Service
metadata:
  name: node-service
spec:
  type: NodePort
  selector:
    app: node-app
  ports:
    - port: 80
      targetPort: 8080
      nodePort: 30012
---
apiVersion: apps/v1
kind: Deployment
metadata:
  name: node-deployment
spec:
  replicas: 2
  selector:
    matchLabels:
      app: node-app
  template:
    metadata:
      labels:
        app: node-app
    spec:
      containers:
        - name: node-container
          image: gcr.io/kodekloud/centos-ssh-enabled:node
          ports:
            - containerPort: 80

]
kubectl create -f /tmp/nodeapp.yaml
kubectl get deploy 
kubectl get pods 
```