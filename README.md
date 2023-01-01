# KodeKloudEngineer
Task 1:
Create a Linux User with non-interactive shell
ssh 172.16.238.12 -l banner 
sudo adduser ravi -s /sbin/nologin

Task 2:
Linux File Permissions
There are new requirements to automate a backup process that was performed manually by the xFusionCorp Industries system admins team earlier. To automate this task, the team has developed a new bash script xfusioncorp.sh. They have already copied the script on all required servers, however they did not make it executable on one the app server i.e App Server 2 in Stratos Datacenter.

Please give executable permissions to /tmp/xfusioncorp.sh script on App Server 2. Also make sure every user can execute it.
ssh 172.16.238.11 -l steve 
 
cd /tmp 
ls -la 
sudo chmod +x xfusioncorp.sh
sudo chmod +r xfusioncorp.sh
ls -la 

Task 3:
During the daily standup, it was pointed out that the timezone across Nautilus Application Servers in Stratos Datacenter doesn't match with that of the local datacenter's timezone, which is Africa/Ceuta.
Correct the mismatch.

ssh 172.16.238.10 -l tony
ssh 172.16.238.11 -l steve
ssh 172.16.238.12 -l banner
rm -f /etc/localtime
ln -sf /usr/share/zoneinfo/Africa/Ceuta /etc/localtime
or
sudo timedatectl set-timezone Africa/Ceuta

Task 4:
There is a critical issue going on with the Nautilus application in Stratos DC. The production support team identified that the application is unable to connect to the database. After digging into the issue, the team found that mariadb service is down on the database server.
Look into the issue and fix the same.

ssh 172.16.239.10 -l peter 
sudo su -
systemctl status mariadb
systemctl start  mariadb
systemctl status mariadb
systemctl status mariadb -l
cat /var/log/mariadb/mariadb.log
chown mysql:mysql /var/run/mariadb
systemctl restart mariadb

Task 5:
One of the Nautilus developers has copied confidential data on the jump host in Stratos DC. That data must be copied to one of the app servers. Because developers do not have access to app servers, they asked the system admins team to accomplish the task for them.
Copy /tmp/nautilus.txt.gpg file from jump server to App Server 3 at location /home/webapp.

cd /tmp/
ls -l
chmod 777 nautilus.txt.gpg
scp /tmp/nautilus.txt.gpg banner@172.16.238.12:/tmp/
ssh 172.16.238.12 -l banner
cd /tmp
sudo su -
cd /tmp
ls
cp nautilus.txt.gpg /home/webapp/
cd /home/webapp/
ls -l

Task 6:
There is some data on Nautilus App Server 2 in Stratos DC. Data needs to be altered in several of the files. On Nautilus App Server 2, alter the /home/BSD.txt file as per details given below:

a. Delete all lines containing word "following" and save results in /home/BSD_DELETE.txt file. (Please be aware of case sensitivity)
b. Replace all occurrence of word "and" to "them" and save results in /home/BSD_REPLACE.txt file.

Note: Let's say you are asked to replace word to with from. In that case, make sure not to alter any words containing this string; for example upto, contribu to r etc.

ssh steve@172.16.238.11
sudo su -
cd /home/
cp BSD.txt BSD_DELETE.txt
cp BSD.txt BSD_REPLACE.txt

#Delete
fgrep following BSD_DELETE.txt
sed -i '/following/d' BSD_DELETE.txt
fgrep following BSD_DELETE.txt

#Replace
fgrep and BSD_REPLACE.txt
sed -i -r 's/and/them/g' BSD_REPLACE.txt
fgrep them BSD_REPLACE.txt

Task 7:
The system admins team of xFusionCorp Industries has noticed intermittent issues with DNS resolution in several apps . App Server 1 in Stratos Datacenter is having some DNS resolution issues, so we want to add some additional DNS nameservers on this server.

As a temporary fix we have decided to go with Google public DNS (ipv4). Please make appropriate changes on this server.

ssh tony@172.16.238.10
sudo su -
cat /etc/resolv.conf
vi /etc/resolv.conf

search stratos.xfusioncorp.com
nameserver 127.0.0.11
nameserver 8.8.8.8
options ndots:0

Task 8:
The xFusionCorp Industries security team recently did a security audit of their infrastructure and came up with ideas to improve the application and server security. They decided to use SElinux for an additional security layer. They are still planning how they will implement it; however, they have decided to start testing with app servers, so based on the recommendations they have the following requirements:

Install the required packages of SElinux on App server 3 in Stratos Datacenter and disable it permanently for now; it will be enabled after making some required configuration changes on this host. Don't worry about rebooting the server as there is already a reboot scheduled for tonight's maintenance window. Also ignore the status of SElinux command line right now; the final status after reboot should be disabled.

ssh banner@172.16.238.12
sudo su -
yum -y install selinux*
sestatus
cat /etc/selinux/config | grep SELINUX
vi /etc/selinux/config

# SELINUX= can take one of these three values:
SELINUX=disabled
# SELINUXTYPE= can take one of three values:
SELINUXTYPE=targeted

sestatus

Task 9:
During the monthly compliance meeting, it was pointed out that several servers in the Stratos DC do not have a valid banner. The security team has provided serveral approved templates which should be applied to the servers to maintain compliance. These will be displayed to the user upon a successful login.

Update the message of the day on all application and db servers for Nautilus. Make use of the approved template located at /home/thor/nautilus_banner on jump host

sudo su -
cd /home/thor/
scp -r  nautilus_banner  tony@stapp01:/tmp
scp -r  nautilus_banner  steve@stapp02:/tmp
scp -r  nautilus_banner  banner@stapp03:/tmp
ssh peter@stdb01
sudo su -
yum install openssh-clients -y
exit
exit
scp -r  nautilus_banner  peter@stdb01:/tmp

ssh tony@stapp01
sudo su -
mv /tmp/nautilus_banner  /etc/motd
exit
exit

ssh steve@stapp02
sudo su -
mv /tmp/nautilus_banner  /etc/motd
exit
exit

ssh banner@stapp03
sudo su -
mv /tmp/nautilus_banner  /etc/motd
exit
exit

ssh peter@stdb01
sudo su -
mv /tmp/nautilus_banner  /etc/motd
exit
exit


Task 10:
As per details shared by the development team, the new application release has some dependencies on the back end. There are some packages/services that need to be installed on all app servers under Stratos Datacenter. As per requirements please perform the following steps:
a. Install nscd package on all the application servers.
b. Once installed, make sure it is enabled to start during boot.

ssh tony@stapp01
sudo su -
yum install nscd -y
systemctl start nscd
systemctl enable nscd
systemctl status nscd

ssh steve@stapp02
sudo su -
yum install nscd -y
systemctl start nscd
systemctl enable nscd
systemctl status nscd

ssh banner@stapp03
sudo su -
yum install nscd -y
systemctl start nscd
systemctl enable nscd
systemctl status nscd


Task 11:
The Nautilus team doesn't want its data to be accessed by any of the other groups/teams due to security reasons and want their data to be strictly accessed by the devops group of the team.
Setup a collaborative directory /devops/data on Nautilus App 3 server in Stratos Datacenter.
The directory should be group owned by the group devops and the group should own the files inside the directory. The directory should be read/write/execute to the group owners, and others should not have any access

ssh banner@stapp03
sudo su -
mkdir -p /devops/data
ll -lsd /devops/data/
chgrp -R devops /devops/data
chmod -R 2770 /devops/data

Task 12:
The backup server in the Stratos DC contains several template XML files used by the Nautilus application. However, these template XML files must be populated with valid data before they can be used. One of the daily tasks of a system admin working in the xFusionCorp industries is to apply string and file manipulation commands!
Replace all occurances of the string "Sample" to "Software" on the XML file /root/nautilus.xml located in the backup server.

ssh clint@stbkp01
sudo su -
cat /root/nautilus.xml |grep Sample | wc -l
cat /root/nautilus.xml |grep Sample
sed -i 's/Sample/Software/g' /root/nautilus.xml
cat /root/nautilus.xml |grep Software
cat /root/nautilus.xml |grep Software |wc -l
cat /root/nautilus.xml |grep Sample |wc -l

Task 13:
Some users of the monitoring app have reported issues with xFusionCorp Industries mail server. They have a mail server in Stork DC where they are using postfix mail transfer agent. Postfix service seems to fail. Try to identify the root cause and fix it.

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

Task 13:

