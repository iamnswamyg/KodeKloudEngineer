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