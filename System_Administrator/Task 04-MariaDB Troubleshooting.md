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