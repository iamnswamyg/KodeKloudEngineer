The Nautilus system admins team has prepared scripts to automate several day-to-day tasks. They want them to be deployed on all app servers in Stratos DC on a set schedule. Before that they need to test similar functionality with a sample cron job. Therefore, perform the steps below:
a. Install cronie package on all Nautilus app servers and start crond service.
b. Add a cron */5 * * * * echo hello > /tmp/cron_text for root user.

```
#Terminal 1
ssh tony@stapp01
sudo su -
yum install cronie -y
systemctl start crond.service
systemctl status crond.service
crontab -e
*/5 * * * * echo hello > /tmp/cron_text
crontab -l
ll /tmp/

#Terminal 2
ssh steve@stapp02
sudo su -
yum install cronie -y
systemctl start crond.service
systemctl status crond.service
crontab -e
*/5 * * * * echo hello > /tmp/cron_text
crontab -l
ll /tmp/

#Terminal 3
ssh banner@stapp03
sudo su -
yum install cronie -y
systemctl start crond.service
systemctl status crond.service
crontab -e
*/5 * * * * echo hello > /tmp/cron_text
crontab -l
ll /tmp/
```