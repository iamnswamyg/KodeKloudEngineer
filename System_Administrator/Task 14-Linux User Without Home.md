The system admins team of xFusionCorp Industries has set up a new tool on all app servers, as they have a requirement to create a service user account that will be used by that tool. They are finished with all apps except for App Server 1 in Stratos Datacenter.
Create a user named mark in App Server 1 without a home directory.

ssh tony@stapp01
sudo su -
id mark
cat /etc/passwd |grep mark
useradd -M mark
id mark
cat /etc/passwd |grep mark
ll /home