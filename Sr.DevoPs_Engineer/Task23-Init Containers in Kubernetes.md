There are some applications that need to be deployed on Kubernetes cluster and these apps have some pre-requisites where some configurations need to be changed before deploying the app container. Some of these changes cannot be made inside the images so the DevOps team has come up with a solution to use init containers to perform these tasks during deployment. Below is a sample scenario that the team is going to test first.
1. Create a Deployment named as ic-deploy-datacenter.
2. Configure spec as replicas should be 1, labels app should be ic-datacenter, template's metadata lables app should be the same ic-datacenter.
3. The initContainers should be named as ic-msg-datacenter, use image ubuntu, preferably with latest tag and use command '/bin/bash', '-c' and 'echo Init Done - Welcome to xFusionCorp Industries > /ic/blog'. The volume mount should be named as ic-volume-datacenter and mount path should be /ic.
4. Main container should be named as ic-main-datacenter, use image ubuntu, preferably with latest tag and use command '/bin/bash', '-c' and 'while true; do cat /ic/blog; sleep 5; done'. The volume mount should be named as ic-volume-datacenter and mount path should be /ic.
4. Volume to be named as ic-volume-datacenter and it should be an emptyDir type.
Note: The kubectl utility on jump_host has been configured to work with the kubernetes cluster.

```
vi /tmp/init-datacenter.yaml
[
apiVersion: apps/v1
kind: Deployment
metadata:
  name: ic-deploy-datacenter
  labels:
    app: ic-datacenter
spec:
  replicas: 1
  selector:
    matchLabels:
      app: ic-datacenter
  template:
    metadata:
      labels:
        app: ic-datacenter
    spec:
      volumes:
        - name: ic-volume-datacenter
          emptyDir: {}
      initContainers:
        - name: ic-msg-datacenter
          image: ubuntu:latest
          command:
            [
              "/bin/bash",
              "-c",
              "echo Init Done - Welcome to xFusionCorp Industries > /ic/blog",
            ]
          volumeMounts:
            - name: ic-volume-datacenter
              mountPath: /ic

      containers:
        - name: ic-main-datacenter
          image: ubuntu:latest
          command:
            [
              "/bin/bash",
              "-c",
              "while true; do cat /ic/blog; sleep 5; done",
            ]
          volumeMounts:
            - name: ic-volume-datacenter
              mountPath: /ic

]

kubectl create -f /tmp/init-datacenter.yaml
kubectl get deploy
kubectl get pods
kubectl logs -f pod-id
kubectl exec ic-deploy-devops-59554f444-5dbmx -- cat /ic/blog
```