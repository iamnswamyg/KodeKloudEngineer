The System Admin Team of XfusionCorp Industries has installed a backup agent tool on all app servers. As per the tool's requirements, they need to create a user with a non-interactive shell. Therefore, create a user named **ravi** with a non-interactive shell in the app03 server

```
ssh 172.16.238.12 -l banner 
sudo adduser ravi -s /sbin/nologin
```