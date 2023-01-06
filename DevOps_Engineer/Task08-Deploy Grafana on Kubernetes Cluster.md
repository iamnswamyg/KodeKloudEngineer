The Nautilus DevOps teams is planning to set up a Grafana tool to collect and analyze analytics from some applications. They are planning to deploy it on Kubernetes cluster. Below you can find more details.
1.) Create a deployment named grafana-deployment-datacenter using any grafana image for Grafana app. Set other parameters as per your choice.
2.) Create NodePort type service with nodePort 32000 to expose the app.
You need not to make any configuration changes inside the Grafana app once deployed, just make sure you are able to access the Grafana login page.
Note: The kubeclt on jump_host has been configured to work with kubernetes cluster.

```
kubectl get pods
kubectl get services
vi /tmp/grafana.yaml
[
--- 
apiVersion: v1
kind: Service
metadata:
  name: grafana-service-datacenter
spec:
  type: NodePort
  selector:
    app: grafana
  ports:
    - port: 3000
      targetPort: 3000
      nodePort: 32000
---
apiVersion: apps/v1
kind: Deployment
metadata:
  name: grafana-deployment-datacenter
spec:
  selector:
    matchLabels:
      app: grafana
  template:
    metadata:
      labels:
        app: grafana
    spec:
      containers:
        - name: grafana-container-datacenter
          image: grafana/grafana:latest
          ports:
            - containerPort: 3000

]
cat /tmp/grafana.yaml
kubectl create -f /tmp/grafana.yaml
kubectl get service
kubectl get pods
```