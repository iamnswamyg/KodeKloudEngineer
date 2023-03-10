During a recent security audit, the application security team of xFusionCorp Industries found security issues with the Apache web server on Nautilus App Server 1 server in Stratos DC. They have listed several security issues that need to be fixed on this server. Please apply the security settings below:
a. On Nautilus App Server 1 it was identified that the Apache web server is exposing the version number. Ensure this server has the appropriate settings to hide the version number of the Apache web server.
b. There is a website hosted under /var/www/html/official on App Server 1. It was detected that the directory /official lists all of its contents while browsing the URL. Disable the directory browser listing in Apache config.
c. Also make sure to restart the Apache service after making the changes.

```
ssh tony@stapp01
sudo su -
systemctl status httpd
cat /etc/httpd/conf/httpd.conf  |grep ServerTokens
cat /etc/httpd/conf/httpd.conf  |grep ServerSignature
cat /etc/httpd/conf/httpd.conf  |grep FollowSymLinks
vi /etc/httpd/conf/httpd.conf
[
IncludeOptional conf.d/*.conf
ServerTokens Prod
ServerSignature Off
]
vi /etc/httpd/conf/httpd.conf
[
Options FollowSymLinks
]
cat /etc/httpd/conf/httpd.conf  |grep FollowSymLinks
systemctl start httpd
systemctl status httpd
curl -I http://stapp01:8080
curl -I http://stapp01:8080/official
```