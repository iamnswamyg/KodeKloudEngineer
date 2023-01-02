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

#SELINUX= can take one of these three values:
SELINUX=disabled
#SELINUXTYPE= can take one of three values:
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

Task 14:
New tools have been installed on the app server in Stratos Datacenter. Some of these tools can only be managed from the graphical user interface. Therefore, there are requirements for these app servers.
On all App servers in Stratos Datacenter change the default runlevel so that they can boot in GUI (graphical user interface) by default. Please do not try to reboot these servers

ssh tony@stapp01
sudo su -
systemctl get-default
systemctl set-default graphical.target
systemctl status graphical.traget
systemctl start graphical.target
systemctl status graphical.target
systemctl get-default

ssh steve@stapp02
sudo su -
systemctl get-default
systemctl set-default graphical.target
systemctl status graphical.traget
systemctl start graphical.target
systemctl status graphical.target
systemctl get-default

ssh banner@stapp03
sudo su -
systemctl get-default
systemctl set-default graphical.target
systemctl status graphical.traget
systemctl start graphical.target
systemctl status graphical.target
systemctl get-default

Task 15:
A developer javed has been assigned Nautilus project temporarily as a backup resource. As a temporary resource for this project, we need a temporary user for javed. It’s a good idea to create a user with a set expiration date so that the user won't be able to access servers beyond that point.
Therefore, create a user named javed on the App Server 2. Set expiry date to 2021-04-15 in Stratos Datacenter. Make sure the user is created as per standard and is in lowercase.

ssh steve@stapp02
sudo su -
adduser javed
chage -E 2021-04-15 javed    
chage -l javed   

Task 16:
The Nautilus system admins team has prepared scripts to automate several day-to-day tasks. They want them to be deployed on all app servers in Stratos DC on a set schedule. Before that they need to test similar functionality with a sample cron job. Therefore, perform the steps below:
a. Install cronie package on all Nautilus app servers and start crond service.
b. Add a cron */5 * * * * echo hello > /tmp/cron_text for root user.

ssh tony@stapp01
sudo su -
yum install cronie -y
systemctl start crond.service
systemctl status crond.service
crontab -e
*/5 * * * * echo hello > /tmp/cron_text
crontab -l
ll /tmp/

ssh steve@stapp02
sudo su -
yum install cronie -y
systemctl start crond.service
systemctl status crond.service
crontab -e
*/5 * * * * echo hello > /tmp/cron_text
crontab -l
ll /tmp/


ssh banner@stapp03
sudo su -
yum install cronie -y
systemctl start crond.service
systemctl status crond.service
crontab -e
*/5 * * * * echo hello > /tmp/cron_text
crontab -l
ll /tmp/


Task 17:
The system admins team of xFusionCorp Industries has set up some scripts on jump host that run on regular intervals and perform operations on all app servers in Stratos Datacenter. To make these scripts work properly we need to make sure the thor user on jump host has password-less SSH access to all app servers through their respective sudo users (i.e tony for app server 1). Based on the requirements, perform the following:
Set up a password-less authentication from user thor on jump host to all app servers through their respective sudo users.

whoami
ssh-keygen -t rsa
ssh-copy-id  tony@stapp01
ssh-copy-id  steve@stapp02
ssh-copy-id  banner@stapp03
ssh tony@stapp01
whoami
exit
ssh steve@stapp02
whoami
exit
ssh banner@stapp03
whoami
exit

Task 18:
After doing some security audits of servers, xFusionCorp Industries security team has implemented some new security policies. One of them is to disable direct root login through SSH.
Disable direct SSH root login on all app servers in Stratos Datacenter.

ssh tony@stapp01
sudo su -
vi /etc/ssh/sshd_config
#PermitRootLogin yes -> PermitRootLogin no
cat /etc/ssh/sshd_config | grep PermitRootLogin
systemctl restart sshd

ssh steve@stapp02
sudo su -
vi /etc/ssh/sshd_config
#PermitRootLogin yes -> PermitRootLogin no
cat /etc/ssh/sshd_config | grep PermitRootLogin
systemctl restart sshd

ssh banner@stapp03
sudo su -
vi /etc/ssh/sshd_config
#PermitRootLogin yes -> PermitRootLogin no
cat /etc/ssh/sshd_config | grep PermitRootLogin
systemctl restart sshd

Task 19:
There was some users data copied on Nautilus App Server 1 at /home/usersdata location by the Nautilus production support team in Stratos DC. Later they found that they mistakenly mixed up different user data there. Now they want to filter out some user data and copy it to another location. Find the details below:
On App Server 1 find all files (not directories) owned by user javed inside /home/usersdata directory and copy them all while keeping the folder structure (preserve the directories path) to /news directory.

ssh tony@stapp01
sudo su -
ll /home/usersdata/
ll /news/
find /home/usersdata/ -type f -user javed -exec cp --parents {} /news \;
ll /news/home/usersdata/

Task 20:
The system admin team of xFusionCorp Industries has noticed an issue with some servers in Stratos Datacenter where some of the servers are not in sync w.r.t time. Because of this, several application functionalities have been impacted. To fix this issue the team has started using common/standard NTP servers. They are finished with most of the servers except App Server 3. Therefore, perform the following tasks on this server:
Install and configure NTP server on App Server 3.
Add NTP server 3.europe.pool.ntp.org in NTP configuration on App Server 3.
Please do not try to start/restart/stop ntp service, as we already have a restart for this service scheduled for tonight and we don't want these changes to be applied right now.

ssh banner@stapp03
sudo su -
rpm -qa |grep ntp
yum install -y ntp
rpm -qa |grep ntp
vi /etc/ntp.conf
[server 3.europe.pool.ntp.org]
cat /etc/ntp.conf |grep europe.pool
ntpstat
systemctl status ntpd
systemctl enable ntpd
systemctl start  ntpd
systemctl status ntpd
ntpstat


Task 21:
As per new application requirements shared by the Nautilus project development team, serveral new packages need to be installed on all app servers in Stratos Datacenter. Most of them are completed except for net-tools.
Therefore, install the net-tools package on all app-servers.

ssh tony@stapp01
sudo su -
rpm -qa |grep net-tools
yum install -y net-tools
rpm -qa |grep net-tools

ssh steve@stapp02
sudo su -
rpm -qa |grep net-tools
yum install -y net-tools
rpm -qa |grep net-tools

ssh banner@stapp03
sudo su -
rpm -qa |grep net-tools
yum install -y net-tools
rpm -qa |grep net-tools


Task 22:
During a routine security audit, the team identified an issue on the Nautilus App Server. Some malicious content was identified within the website code. After digging into the issue they found that there might be more infected files. Before doing a cleanup they would like to find all similar files and copy them to a safe location for further investigation. Accomplish the task as per the following requirements:
a. On App Server 1 at location /var/www/html/media find out all files (not directories) having .js extension.
b. Copy all those files along with their parent directory structure to location /media on same server.
c. Please make sure not to copy the entire /var/www/html/media directory content.

ssh tony@stapp01
sudo su -
ll /var/www/html/media/
find /var/www/html/media/ -type f -name '*.js'
find /var/www/html/media/ -type f -name '*.js' -exec cp --parents {} /media \; 
ll /media

Task 23:
We are working on hardening Apache web server on all app servers. As a part of this process we want to add some of the Apache response headers for security purpose. We are testing the settings one by one on all app servers. As per details mentioned below enable these headers for Apache:
Install httpd package on App Server 3 using yum and configure it to run on 6100 port, make sure to start its service.
Create an index.html file under Apache's default document root i.e /var/www/html and add below given content in it.
Welcome to the xFusionCorp Industries!
Configure Apache to enable below mentioned headers:
X-XSS-Protection header with value 1; mode=block
X-Frame-Options header with value SAMEORIGIN
X-Content-Type-Options header with value nosniff
Note: You can test using curl on the given app server as LBR URL will not work for this task.

ssh banner@stapp03
sudo su -
yum install httpd -y
vi /etc/httpd/conf/httpd.conf 
[#
#Listen: Allows you to bind Apache to specific IP addresses and/or
#ports, instead of the default. See also the <VirtualHost>
#directive.
#Change this to Listen on specific IP addresses as shown below to
#prevent Apache from glomming onto all bound IP addresses.
#Listen 12.34.56.78:80
Listen 6100]
cat /etc/httpd/conf/httpd.conf  |grep Listen
[# Listen: Allows you to bind Apache to specific IP addresses and/or
#Change this to Listen on specific IP addresses as shown below to 
#Listen 12.34.56.78:80
Listen 6100]
vi /etc/httpd/conf/httpd.conf
<IfModule mod_headers.c>
    Header set X-XSS-Protection: "1; mode=block"
    Header always append X-Frame-Options SAMEORIGIN
    Header set X-Content-Type-Options nosniff
</IfModule>
cat /etc/httpd/conf/httpd.conf  |grep X
[Header set X-XSS-Protection "1; mode=block"
Header always append X-Frame-Options SAMEORIGIN
Header set X-Content-Type-Options nosniff]
ll /var/www/html/
vi /var/www/html/index.html
[Welcome to the xFusionCorp Industries!]
cat /var/www/html/index.html
systemctl start httpd
systemctl status  httpd
curl http://localhost:6100
curl -i http://localhost:6100

Task 24:
We have confidential data that needs to be transferred to a remote location, so we need to encrypt that data.We also need to decrypt data we received from a remote location in order to understand its content.
On storage server in Stratos Datacenter we have private and public keys stored /home/*_key.asc. Use those keys to perform the following actions.
Encrypt /home/encrypt_me.txt to /home/encrypted_me.asc.
Decrypt /home/decrypt_me.asc to /home/decrypted_me.txt. (Passphrase for decryption and encryption is kodekloud).

ssh natasha@ststor01
sudo su -
cd /home/
ll
gpg --import public_key.asc
gpg --import private_key.asc
gpg --list-keys
gpg --list-secret-keys
gpg --encrypt -r kodekloud@kodekloud.com --armor < encrypt_me.txt  -o encrypted_me.asc
gpg --decrypt decrypt_me.asc > decrypted_me.txt
 ll
 cat decrypted_me.txt
 cat decrypt_me.asc
 cat encrypt_me.txt
 cat encrypted_me.asc

Task 25:
The production support team of xFusionCorp Industries is working on developing some bash scripts to automate different day to day tasks. One is to create a bash script for taking websites backup. They have a static website running on App Server 3 in Stratos Datacenter, and they need to create a bash script named official_backup.sh which should accomplish the following tasks. (Also remember to place the script under /scripts directory on App Server 3)
a. Create a zip archive named xfusioncorp_official.zip of /var/www/html/official directory.
b. Save the archive in /backup/ on App Server 3. This is a temporary storage, as backups from this location will be clean on weekly basis. Therefore, we also need to save this backup archive on Nautilus Backup Server.
c. Copy the created archive to Nautilus Backup Server server in /backup/ location.
d. Please make sure script won't ask for password while copying the archive file. Additionally, the respective server user (for example, tony in case of App Server 1) must be able to run it.

ssh banner@stapp03
vi /scripts/official_backup.sh

#!/bin/bash
zip -r /backup/xfusioncorp_official.zip /var/www/html/official
scp /backup/xfusioncorp_official.zip clint@stbkp01:/backup

cat /scripts/official_backup.sh
chmod +x /scripts/official_backup.sh

ssh-keygen
ssh-copy-id clint@stbkp01
ssh clint@stbkp01
logout
cd /scripts
sh official_backup.sh
ll /backup
ssh clint@stbkp01
ll /backup

Task 26:
We have some users on all app servers in Stratos Datacenter. Some of them have been assigned some new roles and responsibilities, therefore their users need to be upgraded with sudo access so that they can perform admin level tasks.
a. Provide sudo access to user ammar on all app servers.
b. Make sure you have set up password-less sudo for the user.

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

Task 27:
The system admins team of xFusionCorp Industries needs to deploy a new application on App Server 3 in Stratos Datacenter. They have some pre-requites to get ready that server for application deployment. Prepare the server as per requirements shared below:
Install and configure nginx on App Server 3.
On App Server 3 there is a self signed SSL certificate and key present at location /tmp/nautilus.crt and /tmp/nautilus.key. Move them to some appropriate location and deploy the same in Nginx.
Create an index.html file with content Welcome! under Nginx document root.
For final testing try to access the App Server 3 link (either hostname or IP) from jump host using curl command. For example curl -Ik https://<app-server-ip>/.

ssh banner@stapp03
sudo su -
yum install   epel-release -y
yum install   nginx -y
vi /etc/nginx/nginx.conf

server {
        listen       80;
        listen       [::]:80;
        server_name  172.16.238.12;
        root         /usr/share/nginx/html;

        # Load configuration files for the default server block.
        include /etc/nginx/default.d/*.conf;

        error_page 404 /404.html;
        location = /404.html {
        }

        error_page 500 502 503 504 /50x.html;
        location = /50x.html {
        }
    }

# Settings for a TLS enabled server.
#
    server {
        listen       443 ssl http2;
        listen       [::]:443 ssl http2;
        server_name  172.16.238.12;
        root         /usr/share/nginx/html;

        ssl_certificate "/etc/pki/CA/certs/nautilus.crt";
        ssl_certificate_key "/etc/pki/CA/private/nautilus.key";
        ssl_session_cache shared:SSL:1m;
        ssl_session_timeout  10m;
        ssl_ciphers HIGH:!aNULL:!MD5;
        ssl_prefer_server_ciphers on;

#        # Load configuration files for the default server block.
        include /etc/nginx/default.d/*.conf;

        error_page 404 /404.html;
            location = /40x.html {
        }

        error_page 500 502 503 504 /50x.html;
            location = /50x.html {
        }
    }

}

ll /usr/share/nginx/html/
rm /usr/share/nginx/html/index.html -y
vi /usr/share/nginx/html/index.html
Welcome!
cat /usr/share/nginx/html/index.html
systemctl start nginx
systemctl status nginx
curl -Ik https://stapp03

Task 28:
The Nautilus devops team got some requirements related to some Apache config changes. They need to setup some redirects for some URLs. There might be some more changes need to be done. Below you can find more details regarding that:
httpd is already installed on app server 3. Configure Apache to listen on port 8081.
Configure Apache to add some redirects as mentioned below:
a.) Redirect http://stapp03.stratos.xfusioncorp.com:<Port>/ to http://www.stapp03.stratos.xfusioncorp.com:<Port>/ i.e non www to www. This must be a permanent redirect i.e 301
b.) Redirect http://www.stapp03.stratos.xfusioncorp.com:<Port>/blog/ to http://www.stapp03.stratos.xfusioncorp.com:<Port>/news/. This must be a temporary redirect i.e 302.

ssh banner@stapp03
sudo su -
rpm -qa |grep httpd
cat /etc/httpd/conf/httpd.conf |grep Listen
vi /etc/httpd/conf/httpd.conf
[Listen 8081]
cat /etc/httpd/conf/httpd.conf |grep Listen
cat /etc/httpd/conf/httpd.conf |grep redirect
ll /etc/httpd/conf.d/

<VirtualHost *:8081>
ServerName stapp03.stratos.xfusioncorp.com
Redirect 301 / http://www.stapp03.stratos.xfusioncorp.com:8081/
</VirtualHost>

<VirtualHost *:8081>
ServerName www.stapp03.stratos.xfusioncorp.com:8081/blog/
Redirect 302 /blog/ http://www.stapp03.stratos.xfusioncorp.com:8081/news/
</VirtualHost>

cat  /etc/httpd/conf.d/main.conf
systemctl restart httpd
systemctl status  httpd
curl http://stapp03.stratos.xfusioncorp.com:8081/
curl http://www.stapp03.stratos.xfusioncorp.com:8081
curl http://www.stapp03.stratos.xfusioncorp.com:8081/blog/
curl http://www.stapp03.stratos.xfusioncorp.com:8081/news/

Task 29:
We have a backup management application UI hosted on Nautilus's backup server in Stratos DC. That backup management application code is deployed under Apache on the backup server itself, and Nginx is running as a reverse proxy on the same server. Apache and Nginx ports are 3004 and 8094, respectively. We have iptables firewall installed on this server. Make the appropriate changes to fulfill the requirements mentioned below:
We want to open all incoming connections to Nginx's port and block all incoming connections to Apache's port. Also make sure rules are permanent.

ssh clint@stbkp01
sudo su -
systemctl status iptables
ss -tlnp |grep http
ss -tlnp |grep nginx
systemctl start iptables
systemctl status iptables
iptables -A INPUT -p tcp --dport 8094 -m conntrack --ctstate NEW,ESTABLISHED -j ACCEPT
iptables -A INPUT -p tcp --dport 3004 -m conntrack --ctstate NEW -j REJECT
iptables -L --line-numbers
iptables -R INPUT 5 -p icmp -j REJECT
service iptables save
iptables -L --line-numbers
yum install telnet-y
telnet stbkp01 3004
telnet stbkp01 8094

Task 30:
The Nautilus DevOps team is ready to launch a new application, which they will deploy on app servers in Stratos Datacenter. They are expecting significant traffic/usage of squid on app servers after that. This will generate massive logs, creating huge log files. To utilise the storage efficiently, they need to compress the log files and need to rotate old logs. Check the requirements shared below:
a. In all app servers install squid package.
b. Using logrotate configure squid logs rotation to monthly and keep only 3 rotated logs.
(If by default log rotation is set, then please update configuration as needed)

ssh tony@stapp01
sudo su -
rpm -qa |grep squid
yum install squid -y
ll /etc/logrotate.d/
cat /etc/logrotate.d/squid
vi /etc/logrotate.d/squid
[monthly
rotate 3]
systemctl start squid
systemctl status squid

ssh steve@stapp02
sudo su -
rpm -qa |grep squid
yum install squid -y
ll /etc/logrotate.d/
cat /etc/logrotate.d/squid
vi /etc/logrotate.d/squid
[monthly
rotate 3]
systemctl start squid
systemctl status squid

ssh banner@stapp03
sudo su -
rpm -qa |grep squid
yum install squid -y
ll /etc/logrotate.d/
cat /etc/logrotate.d/squid
vi /etc/logrotate.d/squid
[monthly
rotate 3]
systemctl start squid
systemctl status squid

Task 31:
The Nautilus production support team and security team had a meeting last month in which they decided to use local yum repositories for maintaing packages needed for their servers. For now they have decided to configure a local yum repo on Nautilus Backup Server. This is one of the pending items from last month, so please configure a local yum repository on Nautilus Backup Server as per details given below.
a. We have some packages already present at location /packages/downloaded_rpms/ on Nautilus Backup Server.
b. Create a yum repo named local_yum and make sure to set Repository ID to local_yum. Configure it to use package's location /packages/downloaded_rpms/.
c. Install package wget from this newly created repo.

ssh clint@stbkp01
sudo su -
yum repolist
vi /etc/yum.repos.d/local_yum.repo
cat /etc/yum.repos.d/local_yum.repo

[local_yum]
name=local_yum
baseurl=file:///packages/downloaded_rpms/
enabled = 1
gpgcheck = 0

yum repolist
yum list
yum install wget
yum list wget

Task 32:

During a recent security audit, the application security team of xFusionCorp Industries found security issues with the Apache web server on Nautilus App Server 1 server in Stratos DC. They have listed several security issues that need to be fixed on this server. Please apply the security settings below:
a. On Nautilus App Server 1 it was identified that the Apache web server is exposing the version number. Ensure this server has the appropriate settings to hide the version number of the Apache web server.
b. There is a website hosted under /var/www/html/official on App Server 1. It was detected that the directory /official lists all of its contents while browsing the URL. Disable the directory browser listing in Apache config.
c. Also make sure to restart the Apache service after making the changes.

ssh tony@stapp01
sudo su -
systemctl status httpd
cat /etc/httpd/conf/httpd.conf  |grep ServerTokens
cat /etc/httpd/conf/httpd.conf  |grep ServerSignature
cat /etc/httpd/conf/httpd.conf  |grep FollowSymLinks
vi /etc/httpd/conf/httpd.conf

IncludeOptional conf.d/*.conf
ServerTokens Prod
ServerSignature Off

cat /etc/httpd/conf/httpd.conf  |grep FollowSymLinks
Options FollowSymLinks

systemctl start httpd
systemctl status httpd
curl -I http://stapp01:8080
curl -I http://stapp01:8080/official

Task 33:
xFusionCorp Industries has planned to set up a common email server in Stork DC. After several meetings and recommendations they have decided to use postfix as their mail transfer agent and dovecot as an IMAP/POP3 server. We would like you to perform the following steps:
Install and configure postfix on Stork DC mail server.
Create an email account john@stratos.xfusioncorp.com identified by ksH85UJjhb.
Set its mail directory to /home/john/Maildir.
Install and configure dovecot on the same server.

 ssh groot@stmail01
 sudo su -
 yum install postfix -y
 yum install dovecot -y
 vi /etc/postfix/main.cf
 [
myhostname = stmail01.stratos.xfusioncorp.com
mydomain = stratos.xfusioncorp.com
myorigin = $mydomain
inet_interfaces = all
#inet_interfaces = localhost
mydestination = $myhostname, localhost.$mydomain, localhost, $mydomain
mynetworks = 172.16.238.0/24, 127.0.0.0/8
home_mailbox = Maildir/
]
cat /etc/postfix/main.cf | grep stmail01.stratos.xfusioncorp.com
cat /etc/postfix/main.cf | grep stratos.xfusioncorp.com
cat /etc/postfix/main.cf | grep myorigin
cat /etc/postfix/main.cf | grep inet_interfaces
cat /etc/postfix/main.cf | grep mydestination
cat /etc/postfix/main.cf | grep mynetworks
cat /etc/postfix/main.cf | grep home_mailbox
systemctl start postfix
systemctl status postfix
useradd john
passwd john
cat /etc/passwd | grep john
ll /home/john
telnet stmail01 25
EHLO localhost
mail from:john@stratos.xfusioncorp.com
rcpt to:john@stratos.xfusioncorp.com
DATA
test mail
.
quit
su - john
mailq
cd Maildir/
ll
cat new/1672676793.V801I3918017M600420.stmail01.stratos.xfusioncorp.com
exit
vi /etc/dovecot/dovecot.conf
[protocols = imap pop3 lmtp]
vi /etc/dovecot/conf.d/10-mail.conf
mail_location = maildir:~/Maildir
vi /etc/dovecot/conf.d/10-auth.conf
auth_mechanisms = plain login
vi /etc/dovecot/conf.d/10-master.con
[# permissions (e.g. 0777 allows everyone full permissions).
  unix_listener auth-userdb {
    #mode = 0666
    user = postfix
    group = postfix
  }]
systemctl start dovecot
systemctl status dovecot
telnet stmail01 110
user john
pass ksH85UJjhb
retr 1
quit
ss -tulnp

Task 34:
The production support team of xFusionCorp Industries has deployed some of the latest monitoring tools to keep an eye on every service, application, etc. running on the systems. One of the monitoring systems reported about Apache service unavailability on one of the app servers in Stratos DC.
Identify the faulty app host and fix the issue. Make sure Apache service is up and running on all app hosts. They might not hosted any code yet on these servers so you need not to worry about if Apache isn't serving any pages or not, just make sure service is up and running. Also, make sure Apache is running on port 6000 on all app servers.

telnet stapp01 6000  //connection refused
telnet stapp02 6000
telnet stapp03 6000

ssh tony@stapp01
sudo su -
systemctl start httpd
systemctl status httpd
netstat -tulnp
ps -ef  |grep sendmail
kill 501 //accepting connections pid
ps -ef  |grep sendmail
systemctl start httpd
systemctl status  httpd
logout
logout
telnet stapp01 6000

Task 35:
The Nautilus application development team has shared that they are planning to deploy one newly developed application on Nautilus infra in Stratos DC. The application uses PostgreSQL database, so as a pre-requisite we need to set up PostgreSQL database server as per requirements shared below:
a. Install and configure PostgreSQL database on Nautilus database server.
b. Create a database user kodekloud_roy and set its password to LQfKeWWxWD.
c. Create a database kodekloud_db1 and grant full permissions to user kodekloud_roy on this database.
d. Make appropriate settings to allow all local clients (local socket connections) to connect to the kodekloud_db1 database through kodekloud_roy user using md5 method (Please do not try to encrypt password with md5sum).
e. At the end its good to test the db connection using these new credentials from root user or server's sudo user.

ssh peter@stdb01
sudo su -
yum -y install postgresql-server postgresql-contrib
postgresql-setup initdb
systemctl enable postgresql
systemctl start postgresql
systemctl status postgresql

sudo -u postgres psql
CREATE USER kodekloud_roy WITH PASSWORD 'LQfKeWWxWD';
CREATE DATABASE kodekloud_db1;
GRANT ALL PRIVILEGES ON DATABASE "kodekloud_db1" to kodekloud_roy;
\q
vi /var/lib/pgsql/data/postgresql.conf
[listen_addresses = 'localhost'  ]
cat /var/lib/pgsql/data/postgresql.conf |grep localhost
vi /var/lib/pgsql/data/pg_hba.conf
[local   all             all                                      md5
host    all             all             127.0.0.1/32             md5
host    all             all             ::1/128                  md5 ]
systemctl restart postgresql
systemctl status postgresql
psql -U kodekloud_roy -d kodekloud_db1 -h 127.0.0.1 -W
\q
psql -U kodekloud_roy -d kodekloud_db1 -h localhost -W
\q



