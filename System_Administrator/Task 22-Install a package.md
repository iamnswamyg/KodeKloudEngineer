As per new application requirements shared by the Nautilus project development team, serveral new packages need to be installed on all app servers in Stratos Datacenter. Most of them are completed except for net-tools.
Therefore, install the net-tools package on all app-servers.

```
# Terminal 1
ssh tony@stapp01
sudo su -
rpm -qa |grep net-tools
yum install -y net-tools
rpm -qa |grep net-tools

# Terminal 2
ssh steve@stapp02
sudo su -
rpm -qa |grep net-tools
yum install -y net-tools
rpm -qa |grep net-tools

# Terminal 3
ssh banner@stapp03
sudo su -
rpm -qa |grep net-tools
yum install -y net-tools
rpm -qa |grep net-tools
```