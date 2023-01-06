The Nautilus DevOps team is working to deploy some tools in Kubernetes cluster. Some of the tools are licence based so that licence information needs to be stored securely within Kubernetes cluster. Therefore, the team wants to utilize Kubernetes secrets to store those secrets. Below you can find more details about the requirements:
We already have a secret key file official.txt under /opt location on jump host. Create a generic secret named official, it should contain the password/license-number present in official.txt file.
Also create a pod named secret-xfusion.
Configure pod's spec as container name should be secret-container-xfusion, image should be centos preferably with latest tag (remember to mention the tag with image). Use sleep command for container so that it remains in running state. Consume the created secret and mount it under /opt/demo within the container.
To verify you can exec into the container secret-container-xfusion, to check the secret key under the mounted path /opt/demo. Before hitting the Check button please make sure pod/pods are in running state, also validation can take some time to complete so keep patience.
Note: The kubectl utility on jump_host has been configured to work with the kubernetes cluster.

```
ll /opt
cat /opt/official.txt
kubectl create secret generic official --from-file=/opt/official.txt
kubectl get secret
vi /tmp/secret-xfusion.yml
[
---
apiVersion: v1
kind: Pod
metadata:
  name: secret-xfusion
  labels:
    name: myapp
spec:
  volumes:
    - name: secret-volume-xfusion
      secret:
        secretName: official
  containers:
    - name: secret-container-xfusion
      image: centos:latest
      command: ["/bin/bash", "-c", "sleep 10000"]
      volumeMounts:
        - name: secret-volume-xfusion
          mountPath: /opt/demo
          readOnly: true

]
kubectl create -f /tmp/secret-xfusion.yml
kubectl get pods
kubectl exec secret-xfusion -- cat /opt/demo/official.txt
```