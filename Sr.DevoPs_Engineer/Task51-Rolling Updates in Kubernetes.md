We have an application running on Kubernetes cluster using nginx web server. The Nautilus application development team has pushed some of the latest changes and those changes need be deployed. The Nautilus DevOps team has created an image nginx:1.18 with the latest changes.
1. Perform a rolling update for this application and incorporate nginx:1.18 image. The deployment name is nginx-deployment
Make sure all pods are up and running after the update.
Note: The kubectl utility on jump_host has been configured to work with the kubernetes cluster.

```
kubectl get deployment nginx-deployment -o yaml
kubectl set image deployment/nginx-deployment nginx-container=nginx:1.18
watch kubectl get pods
kubectl rollout status deployment nginx-deployment
```