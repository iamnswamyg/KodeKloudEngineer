Task 01:
There is some data on App Server 1 in Stratos DC. The Nautilus development team shared some requirement with the DevOps team to alter some of the data as per recent changes. The DevOps team is working to prepare a Puppet programming file to accomplish this. Below you can find more details about the task.
Create a Puppet programming file demo.pp under /etc/puppetlabs/code/environments/production/manifests directory on Puppet master node i.e Jump Server and by using puppet file_line resource perform the following tasks.
We have a file /opt/sysops/demo.txt on App Server 1. Use the Puppet programming file mentioned above to replace line Welcome to Nautilus Industries! to Welcome to xFusionCorp Industries!, no other data should be altered in this file.
Notes: :- Please make sure to run the puppet agent test using sudo on agent nodes, otherwise you can face certificate issues. In that case you will have to clean the certificates first and then you will be able to run the puppet agent test.
:- Before clicking on the Check button please make sure to verify puppet server and puppet agent services are up and running on the respective servers, also please make sure to run puppet agent test to apply/test the changes manually first.
:- Please note that once lab is loaded, the puppet server service should start automatically on puppet master server, however it can take upto 2-3 minutes to start.

```
cd /etc/puppetlabs/code/environments/production/manifests/
ll
vi demo.pp
[
class data_replacer {

  file_line { 'line_replace':

    path => '/opt/sysops/demo.txt',

    match => 'Welcome to Nautilus Industries!',

    line  => 'Welcome to xFusionCorp Industries!',

  }

}

node 'stapp01.stratos.xfusioncorp.com' {

  include data_replacer

}

]
puppet parser validate demo.pp
ssh tony@stapp01
sudo su -
puppet agent -tv
cat /opt/sysops/demo.txt
```

Task02:
Nautilus project developers are planning to start testing on a new project. As per their meeting with the DevOps team, they want to test containerized environment application features. As per details shared with DevOps team, we need to accomplish the following task:
a. Pull busybox:musl image on App Server 3 in Stratos DC and re-tag (create new tag) this image as busybox:blog.

```
ssh banner@stapp03
sudo su -
docker images
docker pull busybox:musl
docker image tag busybox:musl  busybox:blog
docker images
```

Task03:
There is some data on all app servers in Stratos DC. The Nautilus development team shared some requirement with the DevOps team to alter some of the data as per recent changes they made. The DevOps team is working to prepare an Ansible playbook to accomplish the same. Below you can find more details about the task.
Write a playbook.yml under /home/thor/ansible on jump host, an inventory is already present under /home/thor/ansible directory on Jump host itself. Perform below given tasks using this playbook:
We have a file /opt/dba/blog.txt on app server 1. Using Ansible replace module replace string xFusionCorp to Nautilus in that file.
We have a file /opt/dba/story.txt on app server 2. Using Ansiblereplace module replace the string Nautilus to KodeKloud in that file.
We have a file /opt/dba/media.txt on app server 3. Using Ansible replace module replace string KodeKloud to xFusionCorp Industries in that file.
Note: Validation will try to run the playbook using command ansible-playbook -i inventory playbook.yml so please make sure the playbook works this way without passing any extra arguments.

```
cd /home/thor/ansible
ll
cat inventory
vi playbook.yml
[
- name: Ansible replace
  hosts: stapp01,stapp02,stapp03
  become: yes
  tasks:
    - name: blog.txt replacement
      replace:
        path: /opt/dba/blog.txt
        regexp: "xFusionCorp"
        replace: "Nautilus"
      when: inventory_hostname == "stapp01"
    - name: story.txt replacement
      replace:
        path: /opt/dba/story.txt
        regexp: "Nautilus"
        replace: "KodeKloud"
      when: inventory_hostname == "stapp02"
    - name: media.txt replacement
      replace:
        path: /opt/dba/media.txt
        regexp: "KodeKloud"
        replace: "xFusionCorp Industries"
      when: inventory_hostname == "stapp03"
]
ansible-playbook -i inventory playbook.yml
ssh -t tony@stapp01 "cat /opt/dba/blog.txt"
ssh -t steve@stapp02 "cat /opt/dba/story.txt"
```

Task04:
The Nautilus DevOps team is working on to create few jobs in Kubernetes cluster. They might come up with some real scripts/commands to use, but for now they are preparing the templates and testing the jobs with dummy commands. Please create a job template as per details given below:
Create a job countdown-datacenter.
The spec template should be named as countdown-datacenter (under metadata), and the container should be named as container-countdown-datacenter
Use image ubuntu with latest tag only and remember to mention tag i.e ubuntu:latest, and restart policy should be Never.
Use command for i in ten nine eight seven six five four three two one ; do echo $i ; done
Note: The kubectl utility on jump_host has been configured to work with the kubernetes cluster.

```
vi job.yml
[

apiVersion: batch/v1
kind: Job
metadata:
  name: countdown-datacenter
spec:
  template:
    metadata:
      name: countdown-datacenter
    spec:
      containers:
        - name: container-countdown-datacenter
          image: ubuntu:latest
          command: ["/bin/sh", "-c"]
          args:
            [
              "for i in ten nine eight seven six five four three two one ; do echo $i ; done",
            ]
      restartPolicy: Never 
]
kubectl apply -f countdown-datacenter.yml 
```

Task05:
The Nautilus DevOps team has some data on jump host in Stratos DC that they want to copy on all app servers in the same data center. However, they want to create an archive of data and copy it to the app servers. Additionally, there are some specific requirements for each server. Perform the task using Ansible playbook as per requirements mentioned below:
Create a playbook.yml under /home/thor/ansible on jump host, an inventory file is already placed under /home/thor/ansible/ on Jump Server itself.
Create an archive demo.tar.gz (make sure archive format is tar.gz) of /usr/src/data/ directory ( present on each app server ) and copy it to /opt/data/ directory on all app servers. The user and group owner of archive demo.tar.gz should be tony for App Server 1, steve for App Server 2 and banner for App Server 3.
Note: Validation will try to run playbook using command ansible-playbook -i inventory playbook.yml so please make sure playbook works this way, without passing any extra arguments.

```
cd /home/thor/ansible/
ansible all -a "ls -ltr /opt/data" -i inventory
vi playbook.yml
[
- name: Task create archive and copy to host
  hosts: stapp01, stapp02, stapp03
  become: yes
  tasks:
    - name: As per the task create the archive file and set the owner
      archive:
        path: /usr/src/data/
        dest: /opt/data/demo.tar.gz
        format: gz
        force_archive: true
        owner: "{{ ansible_user }}"
        group: "{{ ansible_user }}"
]
cat playbook.yml
ansible-playbook  -i inventory playbook.yml
ansible all -a "ls -ltr /opt/data" -i inventory
```

Task06:
The Nautilus DevOps team is testing applications containerization, which issupposed to be migrated on docker container-based environments soon. In today's stand-up meeting one of the team members has been assigned a task to create and test a docker container with certain requirements. Below are more details:
a. On App Server 1 in Stratos DC pull nginx image (preferably latest tag but others should work too).
b. Create a new container with name blog from the image you just pulled.
c. Map the host volume /opt/data with container volume /tmp. There is an sample.txt file present on same server under /tmp; copy that file to /opt/data. Also please keep the container in running state.

```
ssh tony@stapp01
sudo su -
docker images
docker pull nginx:latest
cp /tmp/sample.txt /opt/data/
docker run --name blog -v /opt/data:/tmp -d -it nginx:latest
docker ps
docker exec -it blog /bin/bash
ls /tmp
```

Task07:
A new MySQL server needs to be deployed on Kubernetes cluster. The Nautilus DevOps team was working on to gather the requirements. Recently they were able to finalize the requirements and shared them with the team members to start working on it. Below you can find the details:
1.) Create a PersistentVolume mysql-pv, its capacity should be 250Mi, set other parameters as per your preference.
2.) Create a PersistentVolumeClaim to request this PersistentVolume storage. Name it as mysql-pv-claim and request a 250Mi of storage. Set other parameters as per your preference.
3.) Create a deployment named mysql-deployment, use any mysql image as per your preference. Mount the PersistentVolume at mount path /var/lib/mysql.
4.) Create a NodePort type service named mysql and set nodePort to 30007.
5.) Create a secret named mysql-root-pass having a key pair value, where key is password and its value is YUIidhb667, create another secret named mysql-user-pass having some key pair values, where frist key is username and its value is kodekloud_rin, second key is password and value is YchZHRcLkL, create one more secret named mysql-db-url, key name is database and value is kodekloud_db4
6.) Define some Environment variables within the container:
a) name: MYSQL_ROOT_PASSWORD, should pick value from secretKeyRef name: mysql-root-pass and key: password
b) name: MYSQL_DATABASE, should pick value from secretKeyRef name: mysql-db-url and key: database
c) name: MYSQL_USER, should pick value from secretKeyRef name: mysql-user-pass key key: username
d) name: MYSQL_PASSWORD, should pick value from secretKeyRef name: mysql-user-pass and key: password
Note: The kubectl utility on jump_host has been configured to work with the kubernetes cluster.

```
kubectl get all
kubectl create secret generic mysql-root-pass --from-literal=password=YUIidhb667
kubectl create secret generic mysql-user-pass --from-literal=username=kodekloud_rin --from-literal=password=YchZHRcLkL
kubectl create secret generic mysql-db-url --from-literal=database=kodekloud_db4
kubectl get secret
vi /tmp/mysql.yml
[
---                                                                                           
apiVersion: v1                                                                                
kind: PersistentVolume                                                                        
metadata:                                                                                     
  name: mysql-pv                                                                              
spec:                                                                                         
  capacity:                                                                                   
    storage: 250Mi     
  accessModes:                                                                                
    - ReadWriteOnce                                                                           
  hostPath:                                                                                   
    path: "/var/lib/mysql"                                                                    
---                                                                                           
apiVersion: v1                                                                                
kind: PersistentVolumeClaim                                                                   
metadata:                                                                                     
  name: mysql-pv-claim                                                                        
spec:                                                                                         
  accessModes:                                                                                
    - ReadWriteOnce                                                                           
  resources:                                                                                  
    requests:                                                                                 
      storage: 250Mi                                                                          
---
apiVersion: v1
kind: Service
metadata:
  name: mysql
spec:
  type: NodePort
  selector:
    app: mysql
  ports:
    - port: 3306
      targetPort: 3306
      nodePort: 30007
---	  
apiVersion: apps/v1
kind: Deployment
metadata:
  name: mysql-deployment
  labels:
    app: mysql
spec:
  replicas: 1
  selector:
    matchLabels:
      app: mysql
  template:
    metadata:
      labels:
        app: mysql
    spec:
      volumes:
      - name: mysql-pv
        persistentVolumeClaim:
          claimName: mysql-pv-claim
      containers:
      - name: mysql
        image: mysql:latest
        env:
        - name: MYSQL_ROOT_PASSWORD
          valueFrom:
            secretKeyRef:
              name: mysql-root-pass
              key: password
        - name: MYSQL_DATABASE
          valueFrom:
            secretKeyRef:
              name: mysql-db-url
              key: database
        - name: MYSQL_USER
          valueFrom:
            secretKeyRef:
              name: mysql-user-pass
              key: username
        - name: MYSQL_PASSWORD
          valueFrom:
            secretKeyRef:
              name: mysql-user-pass
              key: password
        volumeMounts:
        - name: mysql-pv
          mountPath: /var/lib/mysql
        ports:
        - containerPort: 3306
          name: mysql

]
cat /tmp/mysql.yml
kubectl create -f /tmp/mysql.yml
kubectl get pv
kubectl get pvc
kubectl get all
kubectl exec -it mysql-deployment-6ccf56667c-bp592 -- /bin/bash
printenv
```

Task08:
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

Task09:
One of the junior DevOps team members was working on to deploy a stack on Kubernetes cluster. Somehow the pod is not coming up and its failing with some errors. We need to fix this as soon as possible. Please look into it.
There is a pod named webserver and the container under it is named as nginx-container. It is using image nginx:latest
There is a sidecar container as well named sidecar-container which is using ubuntu:latest image.
Look into the issue and fix it, make sure pod is in running state and you are able to access the app.
Note: The kubectl utility on jump_host has been configured to work with the kubernetes cluster.

```
kubectl get pods
kubectl describe pod webserver
kubectl edit pod webserver
change image tag from latests to latest and save
kubectl get pods
```

Task10:
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

Task11:
The Nautilus application development team has been working on a project repository /opt/games.git. This repo is cloned at /usr/src/kodekloudrepos on storage server in Stratos DC. They recently shared the following requirements with DevOps team:
a. Create a new branch datacenter in /usr/src/kodekloudrepos/games repo from master and copy the /tmp/index.html file (on storage server itself). Add/commit this file in the new branch and merge back that branch to the master branch. Finally, push the changes to origin for both of the branches.

```
ssh natasha@ststor01
sudo su -
ll /usr/src/kodekloudrepos/games/
cd /usr/src/kodekloudrepos/games/
git status
git checkout -b datacenter
git status
git branch
cp /tmp/index.html  /usr/src/kodekloudrepos/games/
ll /usr/src/kodekloudrepos/games/
git add index.html
git commit -m "added index.html"
git checkout master
git merge datacenter
git push -u origin datacenter
git push -u origin master
git status
```

Task12:
The Nautilus DevOps team is working to deploy some tools in Kubernetes cluster. Some of the tools are licence based so that licence information needs to be stored securely within Kubernetes cluster. Therefore, the team wants to utilize Kubernetes secrets to store those secrets. Below you can find more details about the requirements:
We already have a secret key file media.txt under /opt location on jump host. Create a generic secret named media, it should contain the password/license-number present in media.txt file.
Also create a pod named secret-nautilus.
Configure pod's spec as container name should be secret-container-nautilus, image should be fedora preferably with latest tag (remember to mention the tag with image). Use sleep command for container so that it remains in running state. Consume the created secret and mount it under /opt/apps within the container.
To verify you can exec into the container secret-container-nautilus, to check the secret key under the mounted path /opt/apps. Before hitting the Check button please make sure pod/pods are in running state, also validation can take some time to complete so keep patience.
Note: The kubectl utility on jump_host has been configured to work with the kubernetes cluster.

```
ll /opt
cat /opt/media.txt
kubectl create secret generic media --from-file=/opt/media.txt
kubectl get secret
vi /tmp/secret-pod-nautilus.yml
[
---
apiVersion: v1
kind: Pod
metadata:
  name: secret-pod-nautilus
  labels:
    name: myapp
spec:
  volumes:
    - name: secret-volume-nautilus
      secret:
        secretName: media
  containers:
    - name: secret-container-nautilus
      image: fedora:latest
      command: ["/bin/bash", "-c", "sleep 10000"]
      volumeMounts:
        - name: secret-volume-nautilus
          mountPath: /opt/apps
          readOnly: true

]
kubectl create -f /tmp/secret-pod-nautilus.yml
kubectl get pods
kubectl exec secret-pod-nautilus -- cat /opt/apps/media.txt
```




