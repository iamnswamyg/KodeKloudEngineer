The Nautilus DevOps team is planning to host an application on a nginx-based container. There are number of tickets already been created for similar tasks. One of the tickets has been assigned to set up a nginx container on Application Server 2 in Stratos Datacenter. Please perform the task as per details mentioned below:
a. Pull nginx:alpine-perl docker image on Application Server 2.
b. Create a container named news using the image you pulled.
c. Map host port 5003 to container port 80. Please keep the container in running state.

```
ssh steve@stapp02
sudo su -
docker images
docker pull nginx:alpine-perl
docker images
docker container run -d --name news -p 5003:80 nginx:alpine-perl
docker ps
curl http://localhost:5003
```