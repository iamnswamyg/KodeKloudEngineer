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