The Nautilus Application development team has finished development of one of the applications and it is ready for deployment. It is a guestbook application that will be used to manage entries for guests/visitors. As per discussion with the DevOps team, they have finalized the infrastructure that will be deployed on Kubernetes cluster. Below you can find more details about it.
### BACK-END TIER
1.Create a deployment named redis-master for Redis master.
a.) Replicas count should be 1.
b.) Container name should be master-redis-datacenter and it should use image redis.
c.) Request resources as CPU should be 100m and Memory should be 100Mi.
d.) Container port should be redis default port i.e 6379.
2.Create a service named redis-master for Redis master. Port and targetPort should be Redis default port i.e 6379.
3.Create another deployment named redis-slave for Redis slave.
a.) Replicas count should be 2.
b.) Container name should be slave-redis-datacenter and it should use gcr.io/google_samples/gb-redisslave:v3 image.
c.) Requests resources as CPU should be 100m and Memory should be 100Mi.
d.) Define an environment variable named GET_HOSTS_FROM and its value should be dns.
e.) Container port should be Redis default port i.e 6379.
4.Create another service named redis-slave. It should use Redis default port i.e 6379.
### FRONT END TIER
1.Create a deployment named frontend.
a.) Replicas count should be 3.
b.) Container name should be php-redis-datacenter and it should use gcr.io/google-samples/gb-frontend:v4 image.
c.) Request resources as CPU should be 100m and Memory should be 100Mi.
d.) Define an environment variable named as GET_HOSTS_FROM and its value should be dns.
e.) Container port should be 80.
2.Create a service named frontend. Its type should be NodePort, port should be 80 and its nodePort should be 30009.
Finally, you can check the guestbook app by clicking on + button in the top left corner and Select port to view on Host 1 then enter your nodePort.
You can use any labels as per your choice.
Note: The kubectl utility on jump_host has been configured to work with the kubernetes cluster.

```
kubectl get deploy
kubectl get services
kubectl get pods
mkdir -p /tmp/guestbook
cd /tmp/guestbook
### Back-end-Deploy-Redis-Master
vi Back-end-Deploy-Redis-Master-Guestbook.yml
[
---
apiVersion: apps/v1
kind: Deployment
metadata:
  name: redis-master
spec:
  replicas: 1
  selector:
    matchLabels:
      app: redis-master
      tier: back-end
  template:
    metadata:
      labels:
        app: redis-master
        tier: back-end
    spec:
      containers:
        - name: master-redis-datacenter
          image: redis
          resources:
            requests:
              memory: "100Mi"
              cpu: "100m"
          ports:
            - containerPort: 6379

]
cat Back-end-Deploy-Redis-Master-Guestbook.yml
### Back-end-Service-Redis-Master
vi Back-end-Service-Redis-Master-Guestbook.yml
[
---
apiVersion: v1
kind: Service
metadata:
  name: redis-master
spec:
  type: ClusterIP
  selector:
    app: redis-master
    tier: back-end
  ports:
    - port: 6379
      targetPort: 6379

]
cat Back-end-Service-Redis-Master-Guestbook.yml
### Back-end-Deploy-Redis-Slave
vi Back-end-Deploy-Redis-Slave-Guestbook.yml
[
---
apiVersion: apps/v1
kind: Deployment
metadata:
  name: redis-slave
spec:
  replicas: 2
  selector:
    matchLabels:
      app: redis-slave
      tier: back-end
  template:
    metadata:
      labels:
        app: redis-slave
        tier: back-end
    spec:
      containers:
        - name: slave-redis-datacenter
          image: gcr.io/google_samples/gb-redisslave:v3
          resources:
            requests:
              memory: "100Mi"
              cpu: "100m"
          env:
            - name: GET_HOSTS_FROM
              value: dns
          ports:
            - containerPort: 6379

]
cat Back-end-Deploy-Redis-Slave-Guestbook.yml
### Back-end-service-Redis-Slave
vi Back-end-service-Redis-Slave-Guestbook.yml
[
---
apiVersion: v1
kind: Service
metadata:
  name: redis-slave
spec:
  type: ClusterIP
  selector:
    app: redis-slave
    tier: back-end
  ports:
    - port: 6379
      targetPort: 6379

]
cat Back-end-service-Redis-Slave-Guestbook.yml
### Front-end-Deploy-PHP
vi Front-end-Deploy-PHP-Guestbook.yml
[
---
apiVersion: apps/v1
kind: Deployment
metadata:
  name: frontend
spec:
  replicas: 3
  selector:
    matchLabels:
      app: guestbook
      tier: front-end
  template:
    metadata:
      labels:
        app: guestbook
        tier: front-end
    spec:
      containers:
        - name: php-redis-datacenter
          image: gcr.io/google-samples/gb-frontend:v4
          resources:
            requests:
              memory: "100Mi"
              cpu: "100m"
          env:
            - name: GET_HOSTS_FROM
              value: dns
          ports:
            - containerPort: 80


]
cat Front-end-Deploy-PHP-Guestbook.yml
### Front-end-Service-PHP
vi Front-end-Service-PHP-Guestbook.yml
[
---
apiVersion: v1
kind: Service
metadata:
  name: frontend
spec:
  type: NodePort
  selector:
    app: guestbook
    tier: front-end
  ports:
    - port: 80
      targetPort: 80
      nodePort: 30009

]
kubectl apply -f Back-end-Deploy-Redis-Master-Guestbook.yml
kubectl apply -f Back-end-Deploy-Redis-Slave-Guestbook.yml
kubectl apply -f Back-end-Service-Redis-Master-Guestbook.yml
kubectl apply -f Back-end-service-Redis-Slave-Guestbook.yml
kubectl apply -f Front-end-Deploy-PHP-Guestbook.yml
kubectl apply -f Front-end-Service-PHP-Guestbook.yml
kubectl get deploy
kubectl get pods
kubectl get service 
kubectl exec frontend-7f4f7f84f-8w6bn -- curl -I http://localhost/
```