The Nautilus DevOps team is working on a Kubernetes template to deploy a web application on the cluster. There are some requirements to create/use persistent volumes to store the application code, and the template needs to be designed accordingly. Please find more details below:
1.Create a PersistentVolume named as pv-xfusion. Configure the spec as storage class should be manual, set capacity to 3Gi, set access mode to ReadWriteOnce, volume type should be hostPath and set path to /mnt/dba (this directory is already created, you might not be able to access it directly, so you need not to worry about it).
2.Create a PersistentVolumeClaim named as pvc-xfusion. Configure the spec as storage class should be manual, request 3Gi of the storage, set access mode to ReadWriteOnce.
3.Create a pod named as pod-xfusion, mount the persistent volume you created with claim name pvc-xfusion at document root of the web server, the container within the pod should be named as container-xfusion using image httpd with latest tag only (remember to mention the tag i.e httpd:latest).
4.Create a node port type service named web-xfusion using node port 30008 to expose the web server running within the pod.
Note: The kubectl utility on jump_host has been configured to work with the kubernetes cluster.

```
kubectl get services
kubectl get pods
vi /tmp/persistent-volumes-xfusion.yaml
[
---
apiVersion: v1
kind: PersistentVolume
metadata:
  name: pv-xfusion
spec:
  capacity:
    storage: 3Gi
  accessModes:
    - ReadWriteOnce
  storageClassName: manual
  hostPath:
    path: /mnt/dba
---
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: pvc-xfusion
spec:
  accessModes:
    - ReadWriteOnce
  storageClassName: manual
  resources:
    requests:
      storage: 3Gi
---
apiVersion: v1
kind: Pod
metadata:
  name: pod-xfusion
  labels:
     app: httpd
spec:
  volumes:
    - name: storage-xfusion
      persistentVolumeClaim:
        claimName: pvc-xfusion
  containers:
    - name: container-xfusion
      image: httpd:latest
      ports:
        - containerPort: 80
      volumeMounts:
        - name: storage-xfusion
          mountPath:  /usr/local/apache2/htdocs/
          # nginx mountPath: /usr/share/nginx/html
---                                                                                                           
apiVersion: v1                                                                                                
kind: Service                                                                                                 
metadata:                                                                                                     
  name: web-xfusion                                                                                         
spec:                                                                                                         
   type: NodePort                                                                                             
   selector:                                                                                                  
     app: httpd                                                                                     
   ports:                                                                                                     
     - port: 80                                                                                               
       targetPort: 80                                                                                         
       nodePort: 30008

  
]
 
kubectl create -f /tmp/persistent-volumes-xfusion.yaml
kubectl exec -it pod-xfusion -- bash
curl http://localhost:30008
```