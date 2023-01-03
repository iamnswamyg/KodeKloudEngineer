We have some users on all app servers in Stratos Datacenter. Some of them have been assigned some new roles and responsibilities, therefore their users need to be upgraded with sudo access so that they can perform admin level tasks.
a. Provide sudo access to user ammar on all app servers.
b. Make sure you have set up password-less sudo for the user.

```
# Terminal 1
ssh tony@stapp01
sudo su -
id ammar
su - ammar
sudo cat /etc/sudoers |grep ammar
logout
visudo
[ammar      ALL=(ALL)   NOPASSWD:ALL]
su - ammar
sudo cat /etc/sudoers |grep ammar

# Terminal 2
ssh steve@stapp02
sudo su -
id ammar
su - ammar
sudo cat /etc/sudoers |grep ammar
logout
visudo
[ammar      ALL=(ALL)   NOPASSWD:ALL]
su - ammar
sudo cat /etc/sudoers |grep ammar

# Terminal 3
ssh banner@stapp03
sudo su -
id ammar
su - ammar
sudo cat /etc/sudoers |grep ammar
logout
visudo
[ammar      ALL=(ALL)   NOPASSWD:ALL]
su - ammar
sudo cat /etc/sudoers |grep ammar
```