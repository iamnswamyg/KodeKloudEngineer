Last week the Nautilus DevOps team met with the application development team and decided to containerize several of their applications. The DevOps team wants to do some testing per the following:
Install docker-ce and docker-compose packages on App Server 2.
Start docker service.

```
ssh steve@stapp02
sudo su -
sudo curl -L "https://github.com/docker/compose/releases/download/1.24.1/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose
ll /usr/local/bin/docker-compose
docker-compose --version
yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
yum install docker-ce docker-ce-cli containerd.io
rpm -qa |grep docker
systemctl enable docker
systemctl start  docker
systemctl status  docker
docker --version
docker ps
docker-compose --version
```