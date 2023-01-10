The Nautilus DevOps team needs to set up several docker environments for different applications. One of the team members has been assigned a ticket where he has been asked to create some docker networks to be used later. Complete the task based on the following ticket description:
a. Create a docker network named as news on App Server 3 in Stratos DC.
b. Configure it to use bridge drivers.
c. Set it to use subnet 172.28.0.0/24 and iprange 172.28.0.3/24.

```
ssh banner@stapp03
sudo su -
docker network ls
docker network create -d bridge --subnet=172.28.0.0/24 --ip-range=172.28.0.3/24 news
docker network ls
docker network inspect news
```