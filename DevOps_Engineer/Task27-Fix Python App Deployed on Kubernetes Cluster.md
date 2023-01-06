One of the DevOps engineers was trying to deploy a python app on Kubernetes cluster. Unfortunately, due to some mis-configuration, the application is not coming up. Please take a look into it and fix the issues. Application should be accessible on the specified nodePort.
The deployment name is python-deployment-devops, its using poroko/flask-demo-appimage. The deployment and service of this app is already deployed.
nodePort should be 32345 and targetPort should be python flask app's default port.
Note: The kubectl on jump_host has been configured to work with the kubernetes cluster.

```
kubectl get pods
kubectl get deploy
kubectl get svc
kubectl describe deploy
kubectl get pods
#kubectl logs python-podid
kubectl describe pod python-deployment-devops-54f5444ffb-8qn9r
kubectl edit pod  python-deployment-devops-54f5444ffb-8qn9r //update the image name
kubectl describe svc python-service-devops
kubectl edit svc python-service-devops // update all 8080 ports to python 5000
kubectl describe deploy python-deployment-devops
kubectl edit deploy python-deployment-devops //update the container image name
kubectl get deploy //should be ok after few minutes
```