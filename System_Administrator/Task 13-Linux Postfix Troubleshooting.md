Some users of the monitoring app have reported issues with xFusionCorp Industries mail server. They have a mail server in Stork DC where they are using postfix mail transfer agent. Postfix service seems to fail. Try to identify the root cause and fix it.

```
ssh groot@stmail01
sudo su -
systemctl start postfix
systemctl status postfix -l
cat /etc/postfix/main.cf |grep inet_interface
vi /etc/postfix/main.cf

#inet_interfaces = localhost

systemctl start postfix
systemctl status postfix
exit
exit
```
