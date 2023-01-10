The Nautilus DevOps team is planning to host an application on a nginx-based container. There are number of tickets already been created for similar tasks. One of the tickets has been assigned to set up a nginx container on Application Server 1 in Stratos Datacenter. Please perform the task as per details mentioned below:
a. Pull nginx:alpine-perl docker image on Application Server 1.
b. Create a container named apps using the image you pulled.
c. Map host port 6400 to container port 80. Please keep the container in running state.

```
ssh tony@stapp01
sudo su -
docker pull nginx:alpine-perl
docker container run -d --name apps -p 6400:80 nginx:alpine-perl
docker ps
docker images
curl http://localhost:6400
```