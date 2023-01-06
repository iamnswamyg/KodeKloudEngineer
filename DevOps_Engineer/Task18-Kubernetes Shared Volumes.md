We are working on an application that will be deployed on multiple containers within a pod on Kubernetes cluster. There is a requirement to share a volume among the containers to save some temporary data. The Nautilus DevOps team is developing a similar template to replicate the scenario. Below you can find more details about it.
Create a pod named volume-share-nautilus.
For the first container, use image debian with latest tag only and remember to mention the tag i.e debian:latest, container should be named as volume-container-nautilus-1, and run a sleep command for it so that it remains in running state. Volume volume-share should be mounted at path /tmp/ecommerce.
For the second container, use image debian with the latest tag only and remember to mention the tag i.e debian:latest, container should be named as volume-container-nautilus-2, and again run a sleep command for it so that it remains in running state. Volume volume-share should be mounted at path /tmp/apps.
Volume name should be volume-share of type emptyDir.
After creating the pod, exec into the first container i.e volume-container-nautilus-1, and just for testing create a file ecommerce.txt with any content under the mounted path of first container i.e /tmp/ecommerce.
The file ecommerce.txt should be present under the mounted path /tmp/apps on the second container volume-container-nautilus-2 as well, since they are using a shared volume.
Note: The kubectl utility on jump_host has been configured to work with the kubernetes cluster.

```
kubectl get services
kubectl get pods
vi /tmp/volume-share-nautilus.yaml
[
apiVersion: v1
kind: Pod
metadata:
  name: volume-share-nautilus
  labels:
    name: myapp
spec:
  volumes:
    - name: volume-share
      emptyDir: {}
  containers:
    - name: volume-container-nautilus-1
      image: debian:latest
      command: ["/bin/bash", "-c", "sleep 10000"]
      volumeMounts:
        - name: volume-share
          mountPath: /tmp/ecommerce
    - name: volume-container-nautilus-2
      image: debian:latest
      command: ["/bin/bash", "-c", "sleep 10000"]
      volumeMounts:
        - name: volume-share
          mountPath: /tmp/apps


]
kubectl create -f /tmp/volume-share-nautilus.yaml
kubectl get pods
kubectl exec -it volume-share-nautilus -c volume-container-nautilus-1 -- /bin/bash
echo "Welcome to Nautilus Industries" >/tmp/ecommerce/ecommerce.txt
exit
kubectl exec -it volume-share-nautilus -c volume-container-nautilus-2 -- cat /tmp/apps/ecommerce.txt
```