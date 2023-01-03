New tools have been installed on the app server in Stratos Datacenter. Some of these tools can only be managed from the graphical user interface. Therefore, there are requirements for these app servers.
On all App servers in Stratos Datacenter change the default runlevel so that they can boot in GUI (graphical user interface) by default. Please do not try to reboot these servers

```
#Terminal 1
ssh tony@stapp01
sudo su -
systemctl get-default
systemctl set-default graphical.target
systemctl status graphical.traget
systemctl start graphical.target
systemctl status graphical.target
systemctl get-default

# Terminal 2
ssh steve@stapp02
sudo su -
systemctl get-default
systemctl set-default graphical.target
systemctl status graphical.traget
systemctl start graphical.target
systemctl status graphical.target
systemctl get-default

#Terminal 3
ssh banner@stapp03
sudo su -
systemctl get-default
systemctl set-default graphical.target
systemctl status graphical.traget
systemctl start graphical.target
systemctl status graphical.target
systemctl get-default
```