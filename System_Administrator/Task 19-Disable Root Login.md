After doing some security audits of servers, xFusionCorp Industries security team has implemented some new security policies. One of them is to disable direct root login through SSH.
Disable direct SSH root login on all app servers in Stratos Datacenter.

```
#Terminal 1
ssh tony@stapp01
sudo su -
vi /etc/ssh/sshd_config
#PermitRootLogin yes -> PermitRootLogin no
cat /etc/ssh/sshd_config | grep PermitRootLogin
systemctl restart sshd

#Terminal 2
ssh steve@stapp02
sudo su -
vi /etc/ssh/sshd_config
#PermitRootLogin yes -> PermitRootLogin no
cat /etc/ssh/sshd_config | grep PermitRootLogin
systemctl restart sshd

#Terminal 3
ssh banner@stapp03
sudo su -
vi /etc/ssh/sshd_config
#PermitRootLogin yes -> PermitRootLogin no
cat /etc/ssh/sshd_config | grep PermitRootLogin
systemctl restart sshd
```
