Last week, the Nautilus DevOps team deployed a redis app on Kubernetes cluster, which was working fine so far. This morning one of the team members was making some changes in this existing setup, but he made some mistakes and the app went down. We need to fix this as soon as possible. Please take a look.
The deployment name is redis-deployment. The pods are not in running state right now, so please look into the issue and fix the same.
Note: The kubectl utility on jump_host has been configured to work with the kubernetes cluster.

```
kubectl get deployment
kubectl get deployment redis-deployment
kubectl describe deployment redis-deployment
kubectl get pods
kubectl get pods redis-deployment-8bdf985f7-rl4t2
kubectl describe pods redis-deployment-8bdf985f7-rl4t2
kubectl get configmap
kubectl get configmap redis-config
kubectl describe configmap redis-config
kubectl edit deployment redis-deployment //check typos for config and alpine
kubectl get deploy //wait for few seconds
kubectl get pods
```