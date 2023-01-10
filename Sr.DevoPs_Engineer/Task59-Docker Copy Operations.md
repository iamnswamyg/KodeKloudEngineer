The Nautilus DevOps team has some conditional data present on App Server 3 in Stratos Datacenter. There is a container ubuntu_latest running on the same server. We received a request to copy some of the data from the docker host to the container. Below are more details about the task:
1. On App Server 3 in Stratos Datacenter copy an encrypted file /tmp/nautilus.txt.gpg from docker host to ubuntu_latest container (running on same server) in /home/ location. Please do not try to modify this file in any way.

```
ssh banner@stapp03
sudo su -
docker ps
docker cp /tmp/nautilus.txt.gpg ubuntu_latest:/home/
docker exec ubuntu_latest  ls -ltr /home/
```