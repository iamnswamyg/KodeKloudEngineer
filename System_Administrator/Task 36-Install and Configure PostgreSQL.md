The Nautilus application development team has shared that they are planning to deploy one newly developed application on Nautilus infra in Stratos DC. The application uses PostgreSQL database, so as a pre-requisite we need to set up PostgreSQL database server as per requirements shared below:
a. Install and configure PostgreSQL database on Nautilus database server.
b. Create a database user kodekloud_roy and set its password to LQfKeWWxWD.
c. Create a database kodekloud_db1 and grant full permissions to user kodekloud_roy on this database.
d. Make appropriate settings to allow all local clients (local socket connections) to connect to the kodekloud_db1 database through kodekloud_roy user using md5 method (Please do not try to encrypt password with md5sum).
e. At the end its good to test the db connection using these new credentials from root user or server's sudo user.

```
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
[
listen_addresses = 'localhost'  
]
cat /var/lib/pgsql/data/postgresql.conf |grep localhost
vi /var/lib/pgsql/data/pg_hba.conf
[
local   all             all                                      md5
host    all             all             127.0.0.1/32             md5
host    all             all             ::1/128                  md5 
]
systemctl restart postgresql
systemctl status postgresql
psql -U kodekloud_roy -d kodekloud_db1 -h 127.0.0.1 -W
\q
psql -U kodekloud_roy -d kodekloud_db1 -h localhost -W
\q
```