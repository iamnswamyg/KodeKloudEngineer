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
