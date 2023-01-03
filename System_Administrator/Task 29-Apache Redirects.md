The Nautilus devops team got some requirements related to some Apache config changes. They need to setup some redirects for some URLs. There might be some more changes need to be done. Below you can find more details regarding that:
httpd is already installed on app server 3. Configure Apache to listen on port 8081.
Configure Apache to add some redirects as mentioned below:
a.) Redirect http://stapp03.stratos.xfusioncorp.com:<Port>/ to http://www.stapp03.stratos.xfusioncorp.com:<Port>/ i.e non www to www. This must be a permanent redirect i.e 301
b.) Redirect http://www.stapp03.stratos.xfusioncorp.com:<Port>/blog/ to http://www.stapp03.stratos.xfusioncorp.com:<Port>/news/. This must be a temporary redirect i.e 302.

```
ssh banner@stapp03
sudo su -
rpm -qa |grep httpd
cat /etc/httpd/conf/httpd.conf |grep Listen
vi /etc/httpd/conf/httpd.conf
[Listen 8081]
cat /etc/httpd/conf/httpd.conf |grep Listen
cat /etc/httpd/conf/httpd.conf |grep redirect
ll /etc/httpd/conf.d/
vi  /etc/httpd/conf.d/main.conf
[
<VirtualHost *:8081>
ServerName stapp03.stratos.xfusioncorp.com
Redirect 301 / http://www.stapp03.stratos.xfusioncorp.com:8081/
</VirtualHost>

<VirtualHost *:8081>
ServerName www.stapp03.stratos.xfusioncorp.com:8081/blog/
Redirect 302 /blog/ http://www.stapp03.stratos.xfusioncorp.com:8081/news/
</VirtualHost>
]
cat  /etc/httpd/conf.d/main.conf
systemctl restart httpd
systemctl status  httpd
curl http://stapp03.stratos.xfusioncorp.com:8081/
curl http://www.stapp03.stratos.xfusioncorp.com:8081
curl http://www.stapp03.stratos.xfusioncorp.com:8081/blog/
curl http://www.stapp03.stratos.xfusioncorp.com:8081/news/
```